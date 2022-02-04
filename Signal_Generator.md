`Source Code`
```JS
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity Design is
port ( clk: in std_logic;
        q : out std_logic); 
end Design;

architecture Behavioral of Design is
TYPE state is (zero, one, two);
signal Pr_st1,Pr_st2,Nx_st1,Nx_st2: state;
begin
process(clk)
begin
if (clk'event and clk='1') then
Pr_st1 <= Nx_st1;
end if;
end process;
process(clk)
begin
if (clk'event and clk='1') then
Pr_st2 <= Nx_st2;
end if;
end process;
process(Pr_st1)
begin
case Pr_st1 is 
when zero => q<='1'; Nx_st1<=one;
when one => q<='1' ; Nx_st1<=two;
when two => q<= '0'; Nx_st1 <=zero;
end case;
end process;
process(Pr_st2)
begin
case Pr_st2 is 
when zero => q<='0'; Nx_st2<=one;
when one => q<='1' ; Nx_st2<=two;
when two => q<= '1'; Nx_st2 <=zero;
end case;
end process;
```
`Test Bench`
```css
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;
use IEEE.STD_logic_arith.all;

entity Test_bench is
--  Port ( );
end Test_bench;

architecture Behavioral of Test_bench is
component Design is
port ( clk : in std_logic;
        q : out std_logic); 
end component;
signal clk_tb : std_logic;
signal q_tb : std_logic;
constant period : time := 10ns;
begin
L1 : Design port map(clk_tb, q_tb);
clk_process : Process
begin
clk_tb <= '1';
wait for period/2;
clk_tb <= '0';
wait for period/2;
end process clk_process;
end Behavioral;
```
