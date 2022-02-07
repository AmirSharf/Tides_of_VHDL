`Source Code`

Define `Package`
```Js
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

package My_components is
component OR_gate is
port (x,y : in std_logic;
        z : out std_logic);
end component;
component AND_gate is 
port (x,y : in std_logic;
        z : out std_logic);
end component;
end package;

```
`Design code`
```Js
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;
use work.my_components.all;

entity Design is
port(a,b,c,d : in std_logic;
           y : out std_logic);
end Design;

architecture Behavioral of Design is

signal e,f,g,h : std_logic;
begin
L1: OR_gate port map (a,b,e);
L2: AND_gate port map (c,d,f);
L3: OR_gate port map (a,e,g);
L4: AND_gate port map (c,f,h);
L5: OR_gate port map (g,h,y);
end Behavioral;
```
`Test Bench`
```Js
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity Tb is
--  Port ( );
end Tb;

architecture Behavioral of Tb is
component Design is
port(a,b,c,d : in std_logic;
           y : out std_logic);
end component;

signal a_tb,b_tb,c_tb,d_tb,y_tb : std_logic :='0';
constant period : time := 10ns;
begin
U1: Design port map (a_tb,b_tb,c_tb,d_tb,y_tb);
stim_process : process
begin
wait for period*10;
a_tb <= '1';b_tb <='1';c_tb <='1';d_tb <='1';wait for 50ns;
a_tb <= '0';b_tb <='0';c_tb <='1';d_tb <='1';wait for 50ns;
a_tb <= '0';b_tb <='1';c_tb <='0';d_tb <='1';wait for 50ns;
a_tb <= '0';b_tb <='1';c_tb <='1';d_tb <='1';wait for 50ns;
a_tb <= '1';b_tb <='0';c_tb <='0';d_tb <='1';wait for 50ns;
a_tb <= '1';b_tb <='0';c_tb <='1';d_tb <='1';wait for 50ns;
a_tb <= '1';b_tb <='1';c_tb <='0';d_tb <='1';wait for 50ns;
a_tb <= '0';b_tb <='0';c_tb <='1';d_tb <='0';wait for 50ns;

end process;
end Behavioral;
```
