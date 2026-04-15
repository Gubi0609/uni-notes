**The code for the modules explained below can be seen in the appendix attached at the bottom**
# Keypad
![[Pasted image 20260415102028.png|1000]]

The keypad driver has the following
- Inputs:
	- `rows_in` - The rows from the real life keypad that drives a row low, when a key is pressed.
	- `clock` - The clock used to synchronize everything and step through the keypad columns.
	- `reset` - A reset pin to reset the keypad driver to its start state..
- Outputs:
	- `intr` - An interrupt signal, that will send a high pulse, the width of a clock pulse, when a button is pressed.
	- `key_pressed` - The translated key that has been pressed, translated from 4 bit row/column structure to a binary number representing the number on the corresponding key.
	- `cols_out` - The columns of the real life keypad. This is used to cycle through which column will be pulled low (keypad is active low)

The keypad driver works using a 4 bit counter, that increments by 1 for each clock pulse. The counters output is then split in two, with the lower 2 bits (bits 1 to 0) representing the column currently being read, and the upper 2 bits (bits 3 to 2) representing the row. 
- The lower 2 bits are fed into a 2 to 4 decoder, which outputs a low signal, driving the keypad columns. 
- The upper 2 bits are used as the select pin for a 4 to 1 MUX, with the data input for the MUX being the 4 bit row read from the keypad. 
- Since the rows are active low, the MUX will output the inverted input of the row bit currently being selected by the upper 2 bits from the counter. If a row is low (button being pushed), the MUX outputs a high signal.
- The high signal is used as the data input for the D Flip Flop before the `intr` output, the enable pin for the D Latch before the `key_pressed` output, and also the a port of the AND gate.
- The MUX signal is also fed through an inverter to the counter enable pin, thus freezing the counter if a button is being pressed.
- The D Flip Flop is used together with the AND gate to send a pulse the moment a button has been pressed. Since the D Flip Flop activates on a clock signal, the output `qbar` will be the state of the MUX on the last clock signal. Combined with the AND gate, this produces a pulse, which will only be high, if the MUX was low on the last clock pulse and high on the current clock pulse (A change in its state meaning a button is pushed).
- A keypad translator is used to translate from the row/column output from the counter to a binary number representing the actual value on the pressed key. The letters A - F are represented as numbers 10 - 15.
- Since the D Latch's enable pin is connected to the MUX, it will only be activated when a button has been pushed. This stops the keypad translated output from going out while the counter is counting, and only allows a new output when it has been activated.

# 7-Segment Display Driver
![[Pasted image 20260415102051.png|1000]]

The 7-Segment Display driver has the following
- Inputs:
	- `clock` - The clock used to synchronize the entire system
	- `decimal` - A 6 bit decimal, allowing for numbers as large as 63.
- Outputs:
	- `CAT` - The display selector for the physical display. This changes directly with the `clock` cycle
	- `SSD` - The output for the 7-Segment Display, properly representing a 0 - 9 number on a 7-Segment Display

The SSD driver works by feeding the `decimal` number to be displayed into a BCD encoder.
- The purpose of the BCD encoder is to split the decimal number into the one's and tenth's place. This is done through `mod` division and normal division.
- The one's and tenth's place of the decimal number is then converted into the SSD format, allowing for display on a 7-Segment Display. They are done so separately.
- Each SSD number is then fed into a MUX with two inputs and a select pin. This will alternate which is output with each clock cycle.
- The switch is done in synchronization of the `CAT` output, to ensure that the one's place is displayed on the right hand side 7-Segment Display and the tenth's place is displayed on the left hand side 7-Segment Display.

# Finite State Machine Lock
![[Pasted image 20260415130359.png|1000]]

The lock is implemented using a finite state machine with a total of 9 states. If the correct pin is inserted, the state machine will cycle through the states s0, s1, s2, s4, s4 with the last state (s4) being the unlocking state. Upon pressing the `*` key while unlocked, the system will go into an in
# Finite State Machine Lock with Counter
![[Pasted image 20260415102119.png|1000]]

The FSM lock from above is now combined with a counter, that will reset the lock to the locked stated upon counting to 30.

The FSM lock with counter module has the following
- Inputs:
	- `clk` - The clock used for the rest of the system.
	- `intr` - The interrupt pin from the keypad used to signal that a key has been pressed
	- `key_input` - The pressed key from the keypad
	- `reset` - A reset pin to reset the system to its starting state
- Outputs:
	- `lock` - The system is locked, when this output is high
	- `unlock` - The system is unlocked, when this output is high
	- `cnt_value` - The value of the counter used to re-lock the system. This will be used to display the timer on the 7-Segment Display

The FSM lock works as described in the finite state machine above. It takes an interrupt as an input from the keypad as to not read the pressed key input multiple times per second. This ensures that the user has time to press and release a button.
- When the system unlocks, the enable pin for the counter is driven high, thus activating the counter. The counters input is simultaneously output to `cnt_value` and used as an input for the comparator.
- The comparator compares the counter value with a target value. Since we want the system to reset after 30 seconds, the target value is 30.
- When the counter reaches 30, the output from the comparator will be high, thus reseting the FSM lock through an OR gate. The OR gate is used to also allow reset using the `reset` input pin.
- A clock divider is used to change the clock frequency from 10 kHz, which the rest of the system uses, to 1 Hz, thus only activating the counter one time every second.
- The reset pin from the counter is connected through an OR gate to both the `reset` input pin and the `lock` output from the FSM lock - thus reseting the counter, when the system locks.

# Entire system
![[Pasted image 20260415102209.png|1000]]

The entire system can now be put together.
- Inputs:
	- `jb_in` - The rows of the keypad, attached to the PMOD B pins on the physical board.
	- `sysclk` - The system clock of the board. This has a clock cycle of 125 MHz.
	- `btn_0` - Button 0 on the physical board. This will be used as a reset button.
- Outputs:
	- `ja_cat` - The `CAT` pin for the 7-Segment Display, attached to the PMOD A pins on the physical board.
	- `ja` - The 7-Segment Display output used to drive the display
	- `jb_out` - The columns of the keypad, attached to the PMOD B pins on the physical board.
	- `led_0` - LED 0 on the physical board. Used to display the system being in the locked state.
	- `led_1` - LED 1 on the physical board. Used to display the system being in the unlocked state.

- Since `sysclk` runs on a 125 MHz clock cycle, which is a little high for our system, we use a clock divider to convert it to a 10 kHz clock cycle. This drives all the modules in the system, that uses a clock.
- From left to right we see again the combination of a D Flip Flop and an AND gate. If we look back at the `intr` pin from the keypad driver, we will remember, that it is used to send a pulse, when the `d` input to the D Flip Flop changes to high. We use this with the `a` pin of the AND gate and `d` pin of the D Flip Flop connected to the `lock` output from the FSM lock to reset the keypad, when the system changes from unlocked state to locked state. This is done to ensure, that the last key of the pin-code is never displayed on the 7-Segment Display while the system is locked - thus never revealing any part of the pin-code.
- We notice also, that the `key_pressed` output from the keypad driver and the `cnt_value` output of the FSM lock are both inserted into a 2 input MUX, with the `sel` pin being the `unlock` output of the FSM lock. This is done, so that when the system is locked, the digits displayed on the 7-Segment Display are the inputs from the keypad, while when the system is unlocked, the inputs from the keypad are irrelevant, so we instead show the timer value for when the system will re-lock.

# Simulation
![[Pasted image 20260415120732.png|1500]]

For the simulation a modified block diagram from the one above was designed. This was done, as a new module, `pad_mod` was used to drive the keypad driver. This allowed for a single input `key_pressed`, that could be changed during simulation to mimic the input of a key.
As can be seen from the simulation above, the system was run for multiple clock cycles. The clock divider that converted from 125 MHz to 10 kHz was also removed from the simulation block diagram, as simulating 125 MHz clocks would require a lot of computation and time.
- From the simulation, it can be seen, that for the first 16 clock cycles, there is no input through `key_pressed`. For the next 17 clock cycles, `key_pressed` is set to binary value `10000`, which is row 0, column 0 (counting from 0 - 3). The one `1`, that can be seen, represents that a button is actively being pushed. We hold a button for 17 clock cycles to allow time for the keypad driver to cycle through all rows and columns, thus reading our input.
- We repeat this pattern, inserting the pin-code 1, 2, 3, 4. Upon entering the correct pin-code, we can see that `led_0` (which we will remember is the locked LED) turns off, and `led_1` (which is the unlocked LED) turns on. This demonstrates, that the system will unlock upon receiving the correct pin.

![[Pasted image 20260415121454.png|1500]]

For the sake of demonstration, we also try inserting an incorrect pin-code (in this example 1, 2, 3, 1) to show, that the system will not unlock, if a wrong pin is entered.

## Block Diagram
![[Pasted image 20260415121629.png|1000]]

We can see that the simulation block diagram is much identical to the real life block diagram, with only a few changes.
- Input `jb_in` has been removed, and replaced with `key_pressed` for the `pad_mod` module.
- The clock divider has been removed entirely
- The keypad driver now gets its `rows_in` input from the `pad_mod` module, and feeds its `cols_out` output into `pad_mod`. This is to ensure that they work together in simulating the scan and registration of button presses.
- The output `jb_out` has been removed. This was previously used to drive the columns of the physical keypad.
# Real Life Demonstration
The real life demonstration of the system can be seen through the following link: https://youtube.com/shorts/jHxIEY3PeVs?feature=share

---
# Appendix A - Board Constraints
```xdc
## Clock signal 125 MHz

set_property -dict {PACKAGE_PIN H16 IOSTANDARD LVCMOS33} [get_ports sysclk]
create_clock -add -name sys_clk_pin -period 8.00 -waveform {0 4} [get_ports { sysclk }];

##LEDs

set_property -dict { PACKAGE_PIN R14   IOSTANDARD LVCMOS33 } [get_ports { led_0 }]; #IO_L6N_T0_VREF_34 Sch=led[0]
set_property -dict { PACKAGE_PIN P14   IOSTANDARD LVCMOS33 } [get_ports { led_1 }]; #IO_L6P_T0_34 Sch=led[1]

##Buttons

set_property -dict { PACKAGE_PIN D19   IOSTANDARD LVCMOS33 } [get_ports { btn_0 }]; #IO_L4N_T0_35 Sch=btn[1]
set_property -dict { PACKAGE_PIN D20   IOSTANDARD LVCMOS33 } [get_ports { btn_1 }]; #IO_L4N_T0_35 Sch=btn[1]

##PmodA

set_property -dict { PACKAGE_PIN Y18   IOSTANDARD LVCMOS33 } [get_ports { ja[0] }]; #IO_L17P_T2_34 Sch=ja_p[1]
set_property -dict { PACKAGE_PIN Y19   IOSTANDARD LVCMOS33 } [get_ports { ja[1] }]; #IO_L17N_T2_34 Sch=ja_n[1]
set_property -dict { PACKAGE_PIN Y16   IOSTANDARD LVCMOS33 } [get_ports { ja[2] }]; #IO_L7P_T1_34 Sch=ja_p[2]
set_property -dict { PACKAGE_PIN Y17   IOSTANDARD LVCMOS33 } [get_ports { ja[3] }]; #IO_L7N_T1_34 Sch=ja_n[2]
set_property -dict { PACKAGE_PIN U18   IOSTANDARD LVCMOS33 } [get_ports { ja[4] }]; #IO_L12P_T1_MRCC_34 Sch=ja_p[3]
set_property -dict { PACKAGE_PIN U19   IOSTANDARD LVCMOS33 } [get_ports { ja[5] }]; #IO_L12N_T1_MRCC_34 Sch=ja_n[3]
set_property -dict { PACKAGE_PIN W18   IOSTANDARD LVCMOS33 } [get_ports { ja[6] }]; #IO_L22P_T3_34 Sch=ja_p[4]
set_property -dict { PACKAGE_PIN W19   IOSTANDARD LVCMOS33 } [get_ports { ja_cat }]; #IO_L22N_T3_34 Sch=ja_n[4]

##PmodB

set_property -dict { PACKAGE_PIN W14   IOSTANDARD LVCMOS33 } [get_ports { jb_out[3] }]; #IO_L8P_T1_34 Sch=jb_p[1]
set_property -dict { PACKAGE_PIN Y14   IOSTANDARD LVCMOS33 } [get_ports { jb_out[2] }]; #IO_L8N_T1_34 Sch=jb_n[1]
set_property -dict { PACKAGE_PIN T11   IOSTANDARD LVCMOS33 } [get_ports { jb_out[1] }]; #IO_L1P_T0_34 Sch=jb_p[2]
set_property -dict { PACKAGE_PIN T10   IOSTANDARD LVCMOS33 } [get_ports { jb_out[0] }]; #IO_L1N_T0_34 Sch=jb_n[2]
set_property -dict { PACKAGE_PIN V16   IOSTANDARD LVCMOS33 } [get_ports { jb_in[3] }]; #IO_L18P_T2_34 Sch=jb_p[3]
set_property -dict { PACKAGE_PIN W16   IOSTANDARD LVCMOS33 } [get_ports { jb_in[2] }]; #IO_L18N_T2_34 Sch=jb_n[3]
set_property -dict { PACKAGE_PIN V12   IOSTANDARD LVCMOS33 } [get_ports { jb_in[1] }]; #IO_L4P_T0_34 Sch=jb_p[4]
set_property -dict { PACKAGE_PIN W13   IOSTANDARD LVCMOS33 } [get_ports { jb_in[0] }]; #IO_L4N_T0_34 Sch=jb_n[4]
```
# Appendix B - Code
## And gate
```vhdl
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity AND_Gate is
    Port ( a : in STD_LOGIC;
           b : in STD_LOGIC;
           o : out STD_LOGIC);
end AND_Gate;

architecture rtl of AND_Gate is

begin
o <= a and b;

end rtl;
```

## BCD Encoder
```vhdl
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;
use IEEE.NUMERIC_STD.ALL;

entity BCD_Encoder is
  Port (dec_in : in std_logic_vector(5 downto 0);
        ones_bin : out std_logic_vector(3 downto 0);
        tens_bin : out std_logic_vector(3 downto 0));
end BCD_Encoder;

architecture rtl of BCD_Encoder is
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

## BCD to SSD
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
               "0000001" when others;       
end rtl;
```

## Clock Divider
```vhdl
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;
use IEEE.NUMERIC_STD.ALL;


entity clock_divider is
    Generic (
        clk_in_freq : integer := 125000000; -- default 125 MHz
        clk_out_freq : integer := 10000 -- default 10 kHz
    );
    Port (
        clk_in  : in  std_logic;
        reset   : in  std_logic;
        clk_out : out std_logic
    );
end clock_divider;

architecture rtl of clock_divider is
    constant DIVIDER : integer := clk_in_freq / (clk_out_freq * 2); -- calculate divider
    signal counter : integer range 0 to DIVIDER - 1 := 0;
    signal clk_reg : std_logic := '0';
begin
    process(clk_in, reset)
    begin
        if reset = '1' then
            counter <= 0;
            clk_reg <= '0';
        elsif rising_edge(clk_in) then
            if counter = DIVIDER - 1 then
                counter <= 0;
                clk_reg <= not clk_reg;
            else
                counter <= counter + 1;
            end if;
        end if;
    end process;

    clk_out <= clk_reg;
end rtl;
```

## Comparator
```vhdl
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;
use IEEE.NUMERIC_STD.ALL;

entity comparator is
    Generic (
        input_size  : integer := 5;
        target      : integer := 30
    );
    Port (
        din  : in  std_logic_vector(input_size-1 downto 0);
        dout : out std_logic
    );
end comparator;

architecture rtl of comparator is
begin
    dout <= '1' when unsigned(din) = target else '0';
end rtl;
```

## Counter
```vhdl
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;
use IEEE.NUMERIC_STD.ALL;


entity counter is
    Generic (output_size : integer := 4;
             max_count : integer := 15);
    Port (clk, enable, rst : in std_logic;
          cnt : out std_logic_vector(output_size-1 downto 0));
end counter;

architecture rtl of counter is
    signal cnt_temp: unsigned(output_size-1 downto 0) := (others => '0'); -- Initialize to 0
begin
   process (rst, clk)
   begin
    if (rst = '1') then
        cnt_temp <= (others => '0');
    elsif (enable = '1') then
        if (rising_edge(clk)) then
            if (cnt_temp = to_unsigned(max_count, output_size)) then
                cnt_temp <= (others => '0');
            else
                cnt_temp <= cnt_temp + 1;
            end if;
        end if;        
    end if;
    
   end process;
   cnt <= std_logic_vector(cnt_temp);
end rtl;
```

## Decoder 2 to 4
```vhdl
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity decoder_2to4 is
  Port (bus_in : in std_logic_vector(1 downto 0);
        bus_out : out std_logic_vector(3 downto 0));
end decoder_2to4;

architecture rtl of decoder_2to4 is
begin
with bus_in select
    bus_out <= "1110" when "00",
              "1101" when "01",
              "1011" when "10",
              "0111" when "11",
              "----" when others;
end rtl;
```

## D Flip Flop
```vhdl
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity D_Flip_Flop is
    Port (
        clk  : in  std_logic;
        d    : in  std_logic;
        q    : out std_logic;
        qbar : out std_logic
    );
end D_Flip_Flop;

architecture rtl of D_Flip_Flop is
begin
    process(clk)
    begin
        if rising_edge(clk) then
            q    <= d;
            qbar <= not d;
        end if;
    end process;
end rtl;
```

## D latch
```vhdl
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity D_latch_4bit is
    Port (
        clear  : in  std_logic;
        enable : in  std_logic;
        din    : in  std_logic_vector(3 downto 0);
        dout   : out std_logic_vector(3 downto 0)
    );
end D_latch_4bit;

architecture rtl of D_latch_4bit is
begin
    process(enable, clear, din)
    begin
        if clear = '1' then
            dout <= (others => '0');
        elsif enable = '1' then
            dout <= din;
        end if;
    end process;
end rtl;
```

## FSM lock
```vhdl
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;
use IEEE.NUMERIC_STD.ALL;

entity FSM_lock is
  Generic( PIN_0 : integer := 1; -- first digit
           PIN_1 : integer := 2; -- second digit
           Pin_2 : integer := 3; -- third digit
           PIN_3 : integer := 4  -- fourth digit
           );
  Port (clk : in std_logic;
        rst : in std_logic;
        intr : in std_logic;
        key_in : in std_logic_vector(3 downto 0);
        
        unlock : out std_logic;
        lock : out std_logic);
end FSM_lock;

architecture rtl of FSM_lock is
    type STATE_TYPE is (s0, s1, s2, s3, s4, s5, s6, s7, s_return);
    signal state : STATE_TYPE := s0;
    
    constant KEY_STAR : std_logic_vector(3 downto 0) := "1111"; -- 'F' key will be treated as '*' key

begin
    process(clk, rst)
    begin
        if rst = '1' then
            state <= s0;
        elsif rising_edge(clk) then
            case state is
                when s0 =>
                    if intr = '1' then
                        if key_in = std_logic_vector(to_unsigned(PIN_0, 4)) then
                            state <= s1;
                        elsif key_in = KEY_STAR then
                            state <= s0;
                        else
                            state <= s5;
                        end if;
                    end if;
                when s1 =>
                    if intr = '1' then
                        if key_in = std_logic_vector(to_unsigned(PIN_1, 4)) then
                            state <= s2;
                        else
                            state <= s6;
                        end if;
                    end if;
                when s2 =>
                    if intr = '1' then
                        if key_in = std_logic_vector(to_unsigned(PIN_2, 4)) then
                            state <= s3;
                        else
                            state <= s7;
                        end if;
                    end if;
                when s3 =>
                    if intr = '1' then
                        if key_in = std_logic_vector(to_unsigned(PIN_3, 4)) then
                            state <= s4;
                        else
                            state <= s0;
                        end if;
                   end if;
                when s4 =>
                    if intr = '1' then
                        if key_in = KEY_STAR then
                            state <= s_return;
                        end if;
                    end if;
                when s5 =>
                    if intr = '1' then
                        state <= s6;
                    end if;
                when s6 =>
                    if intr = '1' then
                        state <= s7;
                    end if;
                when s7 =>
                    if intr = '1' then
                        state <= s0;
                    end if;
                when s_return =>
                    state <= s0;
                when others =>
                    state <= state;
            end case;
       end if;                 
    end process;
    unlock <= '1' when state = s4 else '0';
    lock <= '1' when state /= s4 else '0';      
end rtl;
```

## Inverter
```vhdl
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity inverter is
  Port (i : in std_logic;
        o : out std_logic);
end inverter;

architecture rtl of inverter is
begin
    o <= not(i);
end rtl;
```

## Keypad translator
```vhdl
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity keypad_translator is
  Port (key_in : in std_logic_vector(3 downto 0);
        key_out : out std_logic_vector(3 downto 0));
end keypad_translator;

architecture rtl of keypad_translator is
begin
    with key_in select
        key_out <= "0000" when "1100", -- 0
                   "0001" when "0000", -- 1
                   "0010" when "0001", -- 2
                   "0011" when "0010", -- 3
                   "0100" when "0100", -- 4
                   "0101" when "0101", -- 5
                   "0110" when "0110", -- 6
                   "0111" when "1000", -- 7
                   "1000" when "1001", -- 8
                   "1001" when "1010", -- 9
                   "1010" when "0011", -- A
                   "1011" when "0111", -- B
                   "1100" when "1011", -- C
                   "1101" when "1111", -- D
                   "1110" when "1110", -- E
                   "1111" when "1101", -- F
                   (others => '0') when others;
end rtl;
```

## MUX 2 inputs
```vhdl
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity MUX_2in is
  Generic (vector_size : integer := 7);
  Port (din_0 : in std_logic_vector(vector_size-1 downto 0);
        din_1 : in std_logic_vector(vector_size-1 downto 0);
        sel : in std_logic;
        dout : out std_logic_vector(vector_size-1 downto 0));
end MUX_2in;

architecture rtl of MUX_2in is

begin
    with sel select
        dout <= din_0 when '0',
                din_1 when '1',
                (others => '0') when others;
end rtl;
```

## MUX 4 to 1
```vhdl
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity MUX_4to1 is
    Port (
        din  : in  std_logic_vector(3 downto 0);  -- 4 inputs
        sel  : in  std_logic_vector(1 downto 0);  -- 2-bit select
        dout : out std_logic                       -- 1-bit output
    );
end MUX_4to1;

architecture rtl of MUX_4to1 is
begin
    with sel select
        dout <= not din(0) when "00", -- Keypad is active low
                not din(1) when "01",
                not din(2) when "10",
                not din(3) when "11",
                '0'    when others;
end rtl;
```

## OR gate
```vhdl
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity OR_Gate is
    Port ( a : in STD_LOGIC;
           b : in STD_LOGIC;
           o : out STD_LOGIC);
end OR_Gate;

architecture rtl of OR_Gate is

begin
o <= a or b;

end rtl;
```

## Slice
```vhdl
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

-- Uncomment the following library declaration if using
-- arithmetic functions with Signed or Unsigned values
--use IEEE.NUMERIC_STD.ALL;

-- Uncomment the following library declaration if instantiating
-- any Xilinx leaf cells in this code.
--library UNISIM;
--use UNISIM.VComponents.all;

entity slice is
    Generic (
        DIN_WIDTH : integer := 4;  -- input bus width
        DIN_FROM  : integer := 3;  -- top bit
        DIN_TO    : integer := 2   -- bottom bit
    );
    Port (
        din  : in  std_logic_vector(DIN_WIDTH-1 downto 0);
        dout : out std_logic_vector(DIN_FROM-DIN_TO downto 0)
    );
end slice;

architecture rtl of slice is
begin
    dout <= din(DIN_FROM downto DIN_TO);
end rtl;
```
