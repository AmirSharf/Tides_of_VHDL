`Source Code`
```JS
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity Design is
port ( clk,d: in std_logic;
        q : out std_logic); 
end Design;

architecture Behavioral of Design is
TYPE state is (zero, one, two, three);
signal Pr_st,Nx_st: state;
begin
process(clk)
begin
if (clk'event and clk='1') then
Pr_st <= Nx_st;
end if;
end process;
process(Pr_st,d)
begin
case Pr_st is 
when zero => q<='0';
     if(d='1') then
     Nx_st<=one;
     else 
     Nx_st <= zero;
     end if;
when one => q<='0';
     if(d='1') then
     Nx_st<=two;
     else 
     Nx_st <= zero;
     end if;
when two => q<='0';
     if(d='1') then
     Nx_st<=three;
     else 
     Nx_st <= zero;
     end if;
when three => q<='1';
     if(d='0') then
     Nx_st<=zero;
     else 
     Nx_st <= three;
     end if; 
end case;
end process;
end Behavioral;
```
<br>

`Test Bench`
```CSS
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;
use IEEE.STD_logic_arith.all;

entity Test_bench is
--  Port ( );
end Test_bench;

architecture Behavioral of Test_bench is
component Design is
port ( clk,d: in std_logic;
        q : out std_logic); 
end component;
signal clk_tb : std_logic;
signal d_tb : std_logic;
signal q_tb : std_logic;
constant period : time := 10ns;
begin
L1 : Design port map(clk_tb, d_tb, q_tb);
clk_process : Process
begin
clk_tb <= '0';
wait for period/2;
clk_tb <= '1';
wait for period/2;
end process clk_process;

Stim_process : Process
begin
wait for period*5;
d_tb <= '0';
wait for period*5;
d_tb <= '1';
wait for period*5;
end process ;
end Behavioral;
```
`Waveform`
![image](https://user-images.githubusercontent.com/71962033/152560743-02b2caad-a1ea-449e-9daa-594bde425fb4.png)
