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
	- Res