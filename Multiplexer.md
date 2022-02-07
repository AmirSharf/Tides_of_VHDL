`Source Code`
<br><br>
`Mux basic`
```JS
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;
use IEEE.std_logic_arith.all;
use ieee.std_logic_unsigned.all;

entity Mux_basic is
port (a,b,c,d : in std_logic;
        s : in std_logic_vector (1 downto 0);
        y : out std_logic);
end Mux_basic;

architecture Behavioral of Mux_basic is

begin
y <= (a and not s(1) and not s(0)) or
    (b and not s(1) and  s(0)) or
    (c and  s(1) and not s(0)) or
    (d and  s(1) and s(0));
end Behavioral;
```
<br>
`Mux using other operator`

```JS
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;
use ieee.std_logic_arith.all;

entity Mux_Other_Operator is
port (a,b ,c ,d : in std_logic_vector ( 3 downto 0);
       s : in std_logic_vector ( 1 downto 0);
       y : out std_logic_vector (3 downto 0));
end Mux_Other_Operator;

architecture Behavioral of Mux_Other_Operator is

begin
     y<= a when s="00" else
      b when s="01" else
      c when s="10" else
      d when s="11";
-- Method 2
--with s select
--    y <= a when "00",
--      b when "01",
--      c when "10",
--      d when "11",
--     "ZZZZ" WHEN OTHERS;
-- Method 3
-- if (s = "00") then
--   y<=a ;
-- else if (s="01") then
--   y<=b;
--  else if (s="10") then
--    y<=c;
--  else 
--    y<=d;
--  end if;
end Behavioral;
```
`Test Bench`

```CSS
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity Mux_testbench is
--  Port ( );
end Mux_testbench;

architecture Behavioral of Mux_testbench is
component Mux_Other_Operator is 
port (a,b ,c ,d : in std_logic_vector ( 3 downto 0);
       s : in std_logic_vector ( 1 downto 0);
       y : out std_logic_vector (3 downto 0));
       
       end component;
       signal a_tb, b_tb, c_tb,d_tb, y_tb : std_logic_vector := "0000";
       signal s_tb : std_logic_vector (1 downto 0):="00";
begin
L1 : Mux_Other_Operator port map (a_tb,b_tb,c_tb,d_tb,s_tb,y_tb);
a_tb <= "0000" after 80ns , "0010" after 160ns;
b_tb <= "0011" after 80 ns , "0110" after 160ns;
c_tb <= "1000" ;
d_tb <= "1111" after 160ns;
s_tb <= "01" after 80ns ,"10" after 160 ns , "11" after 240 ns ;
end Behavioral;
```
<br>
`Constraints`

```CSS
set_max_delay -from [get_ports {a b c d}] -to [get_ports {y s}] 4.000
```
<br>
<pre>
Timing Summary:-
    WNS(ns)      TNS(ns)  TNS Failing Endpoints  TNS Total Endpoints     
    -------      -------  ---------------------  ------------------- 
     -1.837       -7.305            4                    4 
     
</pre>
