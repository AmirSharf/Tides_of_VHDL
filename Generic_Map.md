`SourceCode`
```JS
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;


entity Design is
generic (k: integer := 7);
port (a,b : in std_logic_vector ( 6 downto 0);
        c : out std_logic_vector( 6 downto 0));
end Design;
architecture Behavioral of Design is
--Call the subprogram using component term
component OR_gate is 
generic (n: integer :=3);
port (a,b : in std_logic_vector ( n-1 downto 0);
        c : out std_logic_vector( n-1 downto 0)); 
end component;
begin
L1 : OR_gate generic map (k) port map(a,b,c);
end Behavioral;
```
`Label`
```JS
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity OR_gate is
generic (n: integer := 3);
port (a,b : in std_logic_vector ( n-1 downto 0);
        c : out std_logic_vector( n-1 downto 0));
end OR_gate;

architecture Behavioral of OR_gate is
begin
c <= a or b;
end Behavioral;
```
`Test Bench`
```css
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity tb is
--  Port ( );
end tb;
architecture Behavioral of tb is
component Design is
port (a,b : in std_logic_vector ( 6 downto 0);
        c : out std_logic_vector( 6 downto 0));
end component;
signal a_tb,b_tb : std_logic_vector(6 downto 0):= "0000000";
signal c_tb : std_logic_vector(6 downto 0):= "0000000";
constant period : time := 10ns;
begin
L1 : Design port map (a_tb,b_tb,c_tb);

stim_process : process
begin
wait for period*10;
a_tb <= "0000000";b_tb <="0000000";
wait for period*10;
a_tb <= "0000000";b_tb <="1100011";
wait for period*10;
a_tb <= "0101010";b_tb <="0110110";
wait for period*10;
a_tb <= "0101010";b_tb <="1010101";
end process;
end Behavioral;
```

`Waveform`
![image](https://user-images.githubusercontent.com/71962033/152408030-4caf4cfe-94c1-4470-9561-55e68d7ea8f2.png)

