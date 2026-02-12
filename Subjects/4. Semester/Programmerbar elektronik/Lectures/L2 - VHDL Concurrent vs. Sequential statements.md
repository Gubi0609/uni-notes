
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

An encoder can be used to minimize the logic behind e.g. a keypad. So say we have a keypad with 9 different buttons. This is a lot of inputs for some systems, or maybe we do not have a lot of space. We can use an _encoder_ to encode the 9 different buttons (states) to only 4 pins / 1 bus of 4 bits.

VHDL code for a priority 4 → 2 decoder
```vhdl
entity PriorityEncoder is
    Port ( D : in STD_LOGIC_VECTOR (3 downto 0);
           Y : out STD_LOGIC_VECTOR (1 downto 0));
end PriorityEncoder;

architecture rtl of PriorityEncoder is

begin
with D select
    Y <= "00" when "0001",
         "01" when "001-",
         "10" when "01--",
         "11" when "1---",
         "--" when others;

end rtl;
```

---
#lecture 