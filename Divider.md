`Source Code`
```JS
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;
use ieee.std_logic_unsigned.all;

entity Divider_counter is
port ( 
       clk : in std_logic;
       output : out std_logic;
       counter_out : out std_logic_vector (2 downto 0));
end Divider_counter;

architecture Behavioral of Divider_counter is
signal divider : std_logic_vector ( 2 downto 0);
signal count : std_logic_vector (2 downto 0);
begin
process (clk)
begin
if rising_edge(clk) then
divider <= divider+'1' ;
end if;
end process;
 output <= divider(2);
 process (divider(2))
 begin
 if rising_edge(divider(2)) then
 count <= count+'1';
 end if;
 end process;
 counter_out <= count;
end Behavioral;

```
`Test Bench`
```css
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity Divider_counter_tb is
--  Port ( );
end Divider_counter_tb;

architecture Behavioral of Divider_counter_tb is
component Divider_counter is
port ( 
       clk : in std_logic;
       output : out std_logic;
       counter_out : out std_logic_vector (2 downto 0));
       end component;
       signal clk_tb :std_logic;
       signal output_tb :std_logic;
       signal counter_out_tb : std_logic_vector (2 downto 0);
       constant period: time := 10ns;
begin
Divider1 : Divider_counter port map (clk_tb,output_tb,counter_out_tb);
clk_process : process
begin
clk_tb <= '0';
wait for period/2;
clk_tb <= '1';
wait for period/2;
end process; 

end Behavioral;
```

<pre>
Timing Summary :-
    WNS(ns)      TNS(ns)  TNS Failing Endpoints  TNS Total Endpoints      
    -------      -------  ---------------------  -------------------       
      8.954       0.000             0                    3
</pre>
