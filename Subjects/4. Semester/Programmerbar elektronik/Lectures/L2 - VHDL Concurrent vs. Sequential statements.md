
---
**Date:** 2026-02-12

## Preparation

>[!TODO] HOMEWORK
>- [ ] Chapter 4 - 5 of [[Free Range VHDL.pdf|the book]]

> [!DANGER] EXERCISES
> - [ ] 

---
# Relevant documents
[[Lecture 2.pdf]]
[[Lab_2.pdf]]

# Topics


# Notes
VHDL programming is all done in _parallel_, because all the gates will work at the same time instead of sequentially.
- Except for _processes_ (like if/else statements)


VHDL code for a DEMUX 4 → 1 using if/else statements
```vhdl
entity DEMUX4_1 is
    Port ( I : in STD_LOGIC;
           sel : in STD_LOGIC_VECTOR (1 downto 0);
           a : out STD_LOGIC;
           b : out STD_LOGIC;
           c : out STD_LOGIC;
           d : out STD_LOGIC);
end DEMUX4_1;

architecture rtl of DEMUX4_1 is

begin
    process(sel, I)
        begin
            if (sel = "00") then a <= I;
            elsif (sel = "01") then b <= I;
            elsif (sel = "10") then c <= I;
            else d <= I;
            end if;
    end process;
    
end rtl;
```


---
#lecture 