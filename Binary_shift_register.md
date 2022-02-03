`Source code`
```JS
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;
use work.circular_shift_register.all;

entity Design is
port (d : in std_logic_vector (3 downto 0);
      load, clk : in std_logic;
      q : out std_logic_vector (3 downto 0));
end Design;

architecture Behavioral of Design is
signal intern,temp : std_logic_vector (3 downto 0);
begin
L1: Mux_gate port map ( temp(0),d(0),Load,intern(3));
L2: D_FF port map (intern(3), clk, temp(3));
L3: Mux_gate port map ( temp(3),d(1),Load,intern(2));
L4: D_FF port map (intern(2), clk, temp(2));
L5: Mux_gate port map ( temp(2),d(2),Load,intern(1));
L6: D_FF port map (intern(1), clk, temp(1));
L7: Mux_gate port map ( temp(1),d(3),Load,intern(0));
L8: D_FF port map (intern(0), clk, temp(0));
q <= temp;
end Behavioral;
```
Define `Mux`
```JS
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity Mux_gate is
port (b,a,s : in std_logic ;
        y : out std_logic);
end Mux_gate;

architecture Behavioral of Mux_gate is
begin
process (b,a,s) is 
begin
if (s='0') then
y <= b;
else
y <= a;
end if;
end process;
end Behavioral;
```
Define `D_FF`
```JS
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity D_FF is
port (d,clk : in std_logic ;
        q : out std_logic);
end D_FF;

architecture Behavioral of D_FF is
begin
process(clk)
begin
if (clk'event and clk = '1') then 
q <= d;
end if;
end process;
end Behavioral;
```
Similarly define all the stimulus that present in the Label section.

`Test Bench`
```css
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity Tb is
--  Port ( );
end Tb;

architecture Behavioral of Tb is
component Design is
port (d : in std_logic_vector (3 downto 0);
      load, clk : in std_logic;
      q : out std_logic_vector (3 downto 0));
end component;
signal d_tb : std_logic_vector(3 downto 0);
signal load_tb, clk_tb : std_logic;
signal q_tb : std_logic_vector(3 downto 0);
constant period : time := 10ns;
begin
L1 : Design port map (d_tb,load_tb,clk_tb,q_tb);
clk_process : process
begin
clk_tb <= '0';
wait for period/2;
clk_tb <= '1';
wait for period/2;
end process;

stim_process : process
begin
wait for period*10;
d_tb <= "0000";load_tb <='0';
wait for period*10;
d_tb <= "0000";load_tb <='1';
wait for period*10;
d_tb <= "0101";load_tb <='0';
wait for period*10;
d_tb <= "0101";load_tb <='1';
wait for period*10;
d_tb <= "1111";load_tb <='0';
wait for period*10;
d_tb <= "1111";load_tb <='1';
end process;
end Behavioral;
```
`Waveform`
![image](https://user-images.githubusercontent.com/71962033/152403970-bf7772c0-e757-4876-84b5-28272c06295a.png)

<pre>
Timing Summary :-
  WNS(ns)      TNS(ns)  TNS Failing Endpoints  TNS Total Endpoints      
  -------      -------  ---------------------  -------------------   
   3.937        0.000            0                    8 
</pre>
