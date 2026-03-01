# Task
- Create a VHDL-based digital clock capable of displaying seconds and minutes
- The design should include appropriate sequential logic (counters, clock dividers, etc.) and any required concurrent processes.
- Perform a functional simulation of the entire clock circuit. The simulation must clearly demonstrate that the clock is counting time correctly for 2 minutes (120 clocks).

# Code

## 0 to 59 Counter
We begin by creating a counter, that will be able to count from 0 to 59, incrementing by one for each clock pulse
```vhdl
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

use IEEE.NUMERIC_STD.ALL;

entity counter_0_to_59 is
    Port (clk, rst : in std_logic;
          cnt : out std_logic_vector(5 downto 0));
end counter_0_to_59;

architecture rtl of counter_0_to_59 is
    signal cnt_temp: unsigned(5 downto 0) := (others => '0'); -- Initialize to 0
begin
   process (rst, clk)
   begin
    if (rst = '1') then
        cnt_temp <= (others => '0');
    elsif (rising_edge(clk)) then
        if (cnt_temp = "111011") then -- 59 in binary
            cnt_temp <= (others => '0');
        else
            cnt_temp <= cnt_temp + 1;
        end if;
    end if;
    
   end process;
   cnt <= std_logic_vector(cnt_temp);
end rtl;

```

We first define our inputs
- `clk` - The clock
- `rst` - A reset for reseting the counter to 0. **Active logical 1**

Then the output
- `cnt` - 6 bit binary number representing the count. The Most Significant Bit (MSB) is placed at the start (**1**00000). Since it is a 6 bit number, it will be able to go from 0 to 63, but numbers 60 to 63 will be unused.

Within the architecture, we use an unsigned signal, called `cnt_temp` with the same binary size as `cnt`, to keep track of the current count. It is initialized to 0.

We use a process, activating on changes in either `rst` or `clk` to run the code.
- If `rst` is **1**, it is active, and we must reset the counter, `cnt_temp`, to 0.
- Otherwise, on a _rising edge_ of the clock, `clk`, we check if the counter, `cnt_temp` is at 59 decimal (111011 binary).
	- If `cnt_temp` is at 59, it must be reset to 0, as a clock goes between 0 to 59
	- Otherwise, `cnt_temp` is incremented by 1.

Outside the process, `cnt_temp` is assigned to `cnt` by converting it from `unsigned` to `std_logic_vector`.

## 60 to 1 Clock Divider
We can reuse the code above for the minutes as well as the seconds, since they both run between 0 to 59. But since the minutes are only incremented every 60 seconds, we must find a way to only toggle a rising edge of the clock every 60 seconds.
```vhdl
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

use IEEE.NUMERIC_STD.ALL;

entity clock_divider_60_to_1 is
  Port (clk_in : in std_logic;
        clk_out : out std_logic);
end clock_divider_60_to_1;

architecture rtl of clock_divider_60_to_1 is
    signal clk_cnt : unsigned(5 downto 0) := (others => '0');
begin
    process (clk_in)
    begin
        if (rising_edge(clk_in)) then
            if (clk_cnt = "111011") then
                clk_cnt <= (others => '0');
                clk_out <= '1';
            else
                clk_cnt <= clk_cnt + 1;
                clk_out <= '0';
            end if;
        end if;       
    end process;
end rtl;
```

Again, we define the inputs
- `clk_in` - The input clock, which is the same clock as the seconds timer will run on.

And the outputs
- `clk_out` - The output clock, which will toggle a rising edge every 60 pulses of `clk_in`.

Within the architecture we again define an unsigned signal, `clk_cnt` to keep track of the number of clock pulses of `clk_in` since the last rising edge of `clk_out`.

We then use a process again, that activates on changes in `clk_in`.
- If we have a _rising edge_ of `clk_in`, we check the state of `clk_cnt` and either
	- Reset `clk_cnt` to 0 and trigger a pulse of `clk_out` **if `clk_cnt` is equal to 59 decimal**.
	- Or **else** we increment `clk_cnt` by 1 and keep `clk_out` set to 0.

# Block Diagram
The above two modules are the essential parts needed for our seconds and minutes timer, and we can now design a block diagram to display the time.

![[Pasted image 20260301161256.png]]

We see, that both the `Seconds_Counter` and `Minutes_Counter` are connected to the same clock, with the small addition of a `Clock_Divider` before `Minutes_Counter`'s `clk` input.
They are also both connected to the same reset, as we will want to reset both of them at the same time to keep them in sync.

We then also have two outputs, both of which are 6 bit logic vectors.
- `sec` - The seconds timer to display the seconds passed.
- `min` - The minutes timer to display the minutes passed.

This forms the basis of our timer module, and we are now ready to test it.

# Simulation
We force the input `reset` to 0, as we do not want to reset our timer.
The input `clock` is forced to a clock, with the leading edge value being 0, and the trailing edge value being 1. Its duty cycle is 50% and it will run a cycle every 100 ns (could be set to 1 second to match the actual display time, but we will leave it at this for now.)

We now run the clock for 120 seconds.
![[Pasted image 20260301162150.png]]

It can however be a bit hard to see, so for demonstrations sake, let us zoom in on each minute change.
![[Pasted image 20260301162255.png]]

We see above the change from minute 0 to minute 1, with the change happening _after_ `3B` hexadecimal seconds or **59** decimal seconds. We see also that the seconds change back to 0.

To again demonstrate, that everything is working as expected, we look further, at the next minute mark.
![[Pasted image 20260301162513.png]]

We see again, that the minutes increment from 1 to 2, with the change happening after another `3B` hexadecimal seconds or **59** decimal seconds. Again, we see that the seconds change back to 0.

# Bonus task
- Format the seconds and minutes outputs so they correspond to the representation used by a 7‑segment display (e.g., BCD encoding or segment-level output) that is provided with the FPGA kit.

To do this, we first design a BCD (Binary-coded decimal) encoding module, and then a module to interface with a 7-segment display.

## BCD Encoding Module
The BCD encoding module is used to convert from a two digit decimal number to two separate numbers in binary, one representing the one's place, and the other representing the ten's place.

```vhdl
ibrary IEEE;
use IEEE.STD_LOGIC_1164.ALL;
use IEEE.NUMERIC_STD.ALL;

entity BCD_encoder_00_to_60 is
  Port (dec_in : in std_logic_vector(5 downto 0);
        ones_bin : out std_logic_vector(3 downto 0);
        tens_bin : out std_logic_vector(3 downto 0));
end BCD_encoder_00_to_60;

architecture rtl of BCD_encoder_00_to_60 is
    signal ones_dec : unsigned(3 downto 0);
    signal tens_dec : unsigned(3 downto 0);
begin
    process (dec_in)
    begin
        ones_dec <= resize(unsigned(dec_in) mod 10, 4);
        tens_dec <= resize(unsigned(dec_in) / 10, 4);
    end process;
    ones_bin <= std_logic_vector(ones_dec);
    tens_bin <= std_logic_vector(tens_dec);

end rtl;
```

Like before, we define the input
- `dec_in` - The decimal number to be split and encoded. It is represented by a 6 bit logic vector to match our counters from before.

And the outputs
- `ones_bin` - The binary number representing the one's place. This is a 4 bit logic vector, meaning that we can theoretically hold the values 0 to 15, but this will not be necessary or used, as we will see in a little bit.
- `tens_bin` - The binary number representing the ten's place. Again, this is a 4 bit logic vector. We would theoretically only need 3 bits to represent the ten's place, as `dec_in` lies within 0 - 63, and a 3 bit number would be able to represent the values 0 - 7. The 4 bit length is chosen to set a standard length for the BCD output, which will be forwarded to the 7-segment display encoder later.

Within the architecture we define an unsigned signal, `ones_dec` to hold the calculated value for the one's place, and another called `tens_dec` to hold the calculated value for the ten's place. Both of these are 4 bits long, which corresponds with the outputs defined before.

We define a process like before, which will trigger upon a change in `dec_in`.
- `ones_dec` is calculated by performing the modulus operation on the input `dec_in` (converted to the `unsigned` type) and 10. By performing modulus on `dec_in` and 10, we essentially divide `dec_in` by 10 and return the leftover. By doing this, we ensure, that it is only (and always) the one's place that is returned.
	- We must also _resize_ the output from this calculation by using `resize(input, size)`, since the input `dec_in` is 6 bits long, and we want it to fit within 4 bits. We thus resize the calculation to 4 bits by typing `resize(calculation, 4)`.
- `tens_dec` is calculated in almost the same way. We again divide `dec_in` (converted to the `unsigned` type) by 10, however this time we return the result as is instead of the leftover. Since VHDL will always truncate (round down) a division, instead of round to the nearest integer, this is essentially a floor division. Since we do not go above 99 (because `dec_in` can only go between 0 to 63), the return from this will always be the ten's place of the input `dec_in`.

Lastly `ones_dec` and `tens_dec` is assigned to `ones_bin` and `tens_bin` by converting them to `std_logic_vector`.

## BCD to 7-segment display encoder
Lastly, we need a module to convert from BCD to the 7-segment display
```vhdl
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity BCD_to_SSD is
  Port (dig_in : in std_logic_vector(3 downto 0);
        ssd_out : out std_logic_vector(6 downto 0));
end BCD_to_SSD;

architecture rtl of BCD_to_SSD is

begin
    with dig_in select
    ssd_out <= "1111110" when "0000", -- 0
               "0110000" when "0001", -- 1
               "1101101" when "0010", -- 2
               "1111001" when "0011", -- 3
               "0110011" when "0100", -- 4
               "1011011" when "0101", -- 5
               "1011111" when "0110", -- 6
               "1110000" when "0111", -- 7
               "1111111" when "1000", -- 8
               "1110011" when "1001", -- 9
               "-------" when others;       
end rtl;
```

For this we need only one input
- `dig_in` - The digit to display. Must be within 0 to 9 to be displayed. This is a 4 bit logic vector, able to represent the numbers 0 - 15.

And one output
- `ssd_out` - The 7-segment display output. This is a 7 bit logic vector with each bit representing a segment on the display. The MSB represents segment **A** and the LSB represents segment **G**. The rest is of course ordered alphabetically.

A diagram of a 7-segment display and the segments' placements can be seen below
![[Pasted image 20260301164923.png]]

Within the architecture, we use a with select statement to check the state of `dig_in`. 
- We go through the numbers 0 - 9, that `dig_in` can lie within, and set the segments accordingly to represent that number. As said before, segment **A** is the MSB of `ssd_out` and segment **G** is the LSB. The rest are ordered alphabetically.
- Since `dig_in` can represent numbers as large as 15, the output of `ssd_out` is set to `"-------"` if the value of `dig_in` is any other than the ones written.

## Block Diagram
![[Pasted image 20260301170735.png]]

Now all the conversion is included, and we outputs from each step for good measure.

## Simulation
