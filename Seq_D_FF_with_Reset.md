`Source Code`
```JS
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;
use IEEE.STD_LOGIC_UNSIGNED.ALL;
use IEEE.STD_LOGIC_ARITH.ALL;

entity D_FF_with_reset is
port (d, clk, rst : in std_logic;
	q: out std_logic);
end D_FF_with_reset;

architecture Behavioral of D_FF_with_reset is

begin
process(clk, rst)
begin
if (rst ='1') then
q<='0';
elsif(clk'event and clk='1') then
q <= d;
end if;
end process;
end Behavioral;
```

`Test Bench`
```css
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;
use IEEE.STD_LOGIC_ARITH.ALL;
use IEEE.STD_LOGIC_UNSIGNED.ALL;

entity D_FF_tb is
--  Port ( );
end D_FF_tb;

architecture Behavioral of D_FF_tb is
component D_FF_with_reset is
port(
      clk,d,rst : in std_logic; 
          q : out std_logic);
end component;

signal d_tb,q_tb,rst_tb : std_logic := '0';
signal clk_tb : std_logic;
--Defining period
constant clk_period : time := 10 ns;

begin
L1 : D_FF_with_reset port map( clk_tb,rst_tb, d_tb, q_tb);

clk_process :process
   begin
    	clk_tb <= '0';
    	wait for clk_period/2; 
    	clk_tb <= '1';
    	wait for clk_period/2;
   end process;
 
stim_process:process
begin
wait for 50ns;
d_tb <= '0';
wait for 50ns;
d_tb <='1';
end process;
end Behavioral;
```
`Constraints`
```JS
create_clock -period 10.000 -name clk -waveform {5.000 10.000} [get_ports clk]
set_input_delay -clock [get_clocks clk] -min -add_delay 0.350 [get_ports d]
set_input_delay -clock [get_clocks clk] -max -add_delay 0.800 [get_ports d]
set_input_delay -clock [get_clocks clk] -min -add_delay 0.350 [get_ports rst]
set_input_delay -clock [get_clocks clk] -max -add_delay 0.900 [get_ports rst]
set_output_delay -clock [get_clocks clk] -min -add_delay -0.150 [get_ports q]
set_output_delay -clock [get_clocks clk] -max -add_delay 0.600 [get_ports q]
```
<pre>
Timing Summary :
     WNS(ns)      TNS(ns)  TNS Failing Endpoints  TNS Total Endpoints       
     -------      -------  ---------------------  -------------------    
      1.176        0.000              0                    3 
</pre>
