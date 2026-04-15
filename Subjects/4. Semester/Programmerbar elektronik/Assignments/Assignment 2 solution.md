


---
# Appendix
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

## MUX 2 inputs