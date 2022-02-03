`Source code`
```JS
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;
use IEEE.STD_LOGIC_ARITH.ALL;
use IEEE.STD_LOGIC_UNSIGNED.ALL;

entity Counter is
port ( clk : in std_logic;
        count : out std_logic_vector(3 downto 0));
end Counter;

architecture Behavioral of Counter is

begin
process(clk)
-- Define var's if present
variable temp: std_logic_vector (3 downto 0) := "0000";
--------------------------
begin
if(clk'event and clk='1') then
temp := temp + 1;
if (temp = "1010") then
temp := "0000";
end if ;
end if;
count <= temp;
end process;
```
`Constraints`
```JS
create_clock -period 10.000 -waveform {2.500 5.000} [get_ports -filter { NAME =~  "*" && DIRECTION == "IN" }]
```
`Test Bench`
```css
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;
use IEEE.STD_LOGIC_ARITH.ALL;
use IEEE.STD_LOGIC_UNSIGNED.ALL;

entity Counter_tb is
--  Port ( );
end Counter_tb;

architecture Behavioral of Counter_tb is
component Counter is  
port ( clk : in std_logic;
        count : out std_logic_vector(3 downto 0));
        end component;

-- Define signal 
signal clk_tb : std_logic;
signal count_tb : std_logic_vector (3 downto 0) := "0000";
constant period : time := 10ns;
begin
L1 : Counter port map (clk_tb, count_tb);
clk_process : Process
begin
clk_tb <= '0';
wait for period/2;
clk_tb <= '1';
wait for period/2;
end process clk_process;

end Behavioral;

```
<pre>
     WNS(ns)      TNS(ns)  TNS Failing Endpoints  TNS Total Endpoints      WHS(ns)      
     -------      -------  ---------------------  -------------------      -------    
      7.997        0.000             0                    8                 0.272 
</pre>
