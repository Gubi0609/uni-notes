# Audiobook Splitting Guide

## Step 0: Check for embedded chapters
Some audiobooks already have chapter markers embedded. Check first:
```bash
ffprobe -i "file.mp3" -print_format json -show_chapters 2>/dev/null
```
If chapters are listed, you can skip to splitting directly. If the list is empty, proceed below.

---

## Step 1: Find chapter timestamps via silence detection

Run silence detection and output in HH:MM:SS format:
```bash
ffmpeg -i "file.mp3" -af silencedetect=noise=-48dB:d=3.2 -f null - 2>&1 | grep "silence_end" | awk '{print $5}' | grep -E '^[0-9]+\.?[0-9]*$' | awk '{secs=int($1); h=int(secs/3600); m=int((secs%3600)/60); s=secs%60; printf "%s -> %02d:%02d:%02d\n", $1, h, m, s}'
```

### Tuning the silence detection
The key parameter is `d=X` (minimum silence duration in seconds):
- Too many splits → increase `d` (try 3.5, 4, 4.5...)
- Too few splits → decrease `d` (try 3.1, 3.15, 3.2...)
- Start with `d=3.2` as a baseline

### Filtering out false splits (close pairs)
If you know the minimum chapter length, filter with:
```bash
... | awk 'NR==1{print; prev=$1; next} $1-prev>=600{print; prev=$1}'
```
Replace `600` with your minimum chapter length in seconds (e.g. 600 = 10 minutes).

### Identifying correct timestamps
- Listen to a few seconds around each candidate timestamp:
  ```bash
  ffmpeg -i "file.mp3" -ss HH:MM:SS -to HH:MM:SS -c copy ~/test.mp3
  ```
- Chapter breaks are usually marked by a pause + narrator announcing "Kapitel X"
- Discard timestamps that are within a minute of each other (false splits)

---

## Step 2: Split the file

Create a split script:
```bash
cat > ~/split_book.sh << 'EOF'
INFILE="$HOME/path/to/file.mp3"
OUTDIR="$HOME/path/to/output"
mkdir -p "$OUTDIR"

ffmpeg -i "$INFILE" -ss 00:00:00 -to 00:00:19 -c copy "$OUTDIR/01 - Bookname.mp3"
ffmpeg -i "$INFILE" -ss 00:00:19 -to 00:20:44 -c copy "$OUTDIR/02 - Bookname.mp3"
# ... one line per chapter ...
ffmpeg -i "$INFILE" -ss HH:MM:SS              -c copy "$OUTDIR/NN - Bookname.mp3"  # last file has no -to

echo "Done!"
EOF

bash ~/split_book.sh
```

**Notes:**
- ffmpeg accepts HH:MM:SS directly for `-ss` and `-to`
- The last file omits `-to` so it runs to the end of the file
- Avoid `~` inside quoted paths in ffmpeg — use `$HOME` instead
- Avoid apostrophes in filenames — rename files before processing if needed:
  ```bash
  mv *Filename*.mp3 simple_name.mp3
  ```

### Merging segments if needed
If two files need to be merged (same chapter split incorrectly):
```bash
ffmpeg -i "01.mp3" -i "02.mp3" -filter_complex "[0:a][1:a]concat=n=2:v=0:a=1" "merged.mp3"
```
For more files, extend the filter: `[0:a][1:a][2:a]concat=n=3:v=0:a=1`

Then re-run silence detection on the merged file to find splits within it,
and add the merged file's start offset to get absolute timestamps:
```
absolute_timestamp = merged_file_start + offset_within_merged
```

---

## Step 3: Tag metadata + embed cover art

Convert cover image to jpg if needed (avif, png, etc.):
```bash
dwebp -i cover.avif -o cover.jpg
```

Create a tagging script:
```bash
cat > ~/tag_book.sh << 'EOF'
OUTDIR="$HOME/path/to/output"
COVER="$HOME/cover.jpg"
TOTAL=24  # total number of files

tag() {
    local num=$1 title=$2 track=$3
    local f="$OUTDIR/$(printf '%02d' $num) - Bookname.mp3"
    local tmp="${f%.mp3}_tmp.mp3"
    ffmpeg -i "$f" -i "$COVER" \
        -map 0:a -map 1 \
        -c copy \
        -id3v2_version 3 \
        -metadata track="$track/$TOTAL" \
        -metadata title="$title" \
        -metadata album="Album name" \
        -metadata artist="Author name" \
        -metadata composer="Narrator name" \
        -metadata date="YYYY" \
        -metadata genre="Genre" \
        -metadata comment="Indlæser: X. Forlag: Y. Lydbog." \
        -metadata:s:v title="Album cover" \
        -metadata:s:v comment="Cover (front)" \
        "$tmp" && mv "$tmp" "$f"
}

tag 1  "Title"     1
tag 2  "Chapter 1" 2
# ... one line per file ...
tag 24 "Outro"     24

echo "Done!"
EOF

bash ~/tag_book.sh
```

---

## Step 4: Embed chapter markers (for audiobook players)

This embeds a single ID3 chapter marker per file so players like Audiobookshelf
and phone apps can navigate by chapter correctly.

```bash
cat > ~/chapter_mark.py << 'EOF'
import os
from mutagen.id3 import ID3, CHAP, CTOC, TIT2, ID3NoHeaderError

OUTDIR = os.path.expanduser("~/path/to/output")

titles = [
    "Title",
    "Chapter 1: Name",
    "Chapter 2: Name",
    # ... one entry per file, in order ...
    "Outro",
]

files = sorted([f for f in os.listdir(OUTDIR) if f.endswith(".mp3")])

for filename, title in zip(files, titles):
    filepath = os.path.join(OUTDIR, filename)
    try:
        tags = ID3(filepath)
    except ID3NoHeaderError:
        tags = ID3()

    for key in list(tags.keys()):
        if key.startswith("CHAP") or key.startswith("CTOC"):
            del tags[key]

    tags.add(CHAP(
        element_id="ch0",
        start_time=0,
        end_time=0xFFFFFFFF,
        start_offset=0xFFFFFFFF,
        end_offset=0xFFFFFFFF,
        sub_frames=[TIT2(encoding=3, text=title)]
    ))

    tags.add(CTOC(
        element_id="toc",
        flags=0x03,
        child_element_ids=["ch0"],
        sub_frames=[TIT2(encoding=3, text=title)]
    ))

    tags.save(filepath)
    print(f"Tagged {filename} -> {title}")

print("Done!")
EOF

python3 ~/chapter_mark.py
```

---

## Quick reference: Common issues

| Problem | Solution |
|--------|----------|
| Too many splits | Increase `d` value in silencedetect |
| Too few splits | Decrease `d` value in silencedetect |
| Apostrophe in filename causes errors | Rename file: `mv *Name*.mp3 simple.mp3` |
| `~` not expanding in ffmpeg path | Use `$HOME` instead of `~` |
| Last file is empty/corrupt | Check that final timestamp doesn't exceed file duration |
| Cover art format not supported | Convert to jpg with ffmpeg first |
| Audiobookshelf not showing chapters | Run the chapter marker Python script (Step 4) |
| mp3splt ignoring min-len parameter | Use ffmpeg silence detection instead |
