`Source Code`
```JS
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;
use IEEE.STD_LOGIC_UNSIGNED.ALL;
use IEEE.STD_LOGIC_ARITH.ALL;

entity D_FF is
port (d,clk : in std_logic;
        q: out std_logic);
end D_FF;

architecture Behavioral of D_FF is

begin
process(clk)
begin
if(clk'event and clk='1') then
q <= d;
end if;
end process;
end architecture;
```

`Test Bench`
```css
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity D_tb is
--  Port ( );
end D_tb;

architecture Behavioral of D_tb is
component D_FF is
port(
      d, clk : in std_logic; 
          q : out std_logic);
end component;

signal d_tb,q_tb : std_logic := '0';
signal clk_tb : std_logic;
--Defining period
constant clk_period : time := 10 ns;

begin
L1 : D_FF port map( d_tb, clk_tb, q_tb);

clk_process: process
   begin
    	clk_tb <= '0';
    	wait for clk_period/2; 
    	clk_tb <= '1';
    	wait for clk_period/2;
   end process clk_process;
 
stim_process: process
begin
wait for 50ns;
d_tb <= '0';
wait for 50ns;
d_tb <='1';
end process stim_process;
end Behavioral;
```
`Constraints`
```JS
set_max_delay -from [get_ports {clk d}] -to [get_ports q] 5.000

create_clock -period 10.000 -name clk -waveform {0.000 5.000} [get_ports clk]
set_input_delay -clock [get_clocks clk] -min -add_delay 0.300 [get_ports d]
set_input_delay -clock [get_clocks clk] -max -add_delay 0.500 [get_ports d]
set_output_delay -clock [get_clocks clk] -min -add_delay -9.600 [get_ports q]
set_output_delay -clock [get_clocks clk] -max -add_delay 5.250 [get_ports q]
```
`Waveform`
![image](https://user-images.githubusercontent.com/71962033/152556290-26555ac7-f5ed-41cf-8125-0a88b0f57f4c.png)

<pre>
Timing Summary :-
    WNS(ns)      TNS(ns)  TNS Failing Endpoints  TNS Total Endpoints      
    -------      -------  ---------------------  -------------------      
    -16.986      -16.986            1                    2 
</pre>
