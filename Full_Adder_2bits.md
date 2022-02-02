`Source Code`
```JS
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity FA is
    Port ( a : in STD_LOGIC;
           b : in STD_LOGIC;
           cin : in STD_LOGIC;
           s : out STD_LOGIC;
           cout : out STD_LOGIC);
end FA;

architecture Behavioral of FA is

begin
s<= a xor b xor cin;
cout<= (a and b) or (b and cin) or (cin and a);

end Behavioral;
```
`Test Bench`
```css
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

-- Uncomment the following library declaration if using
-- arithmetic functions with Signed or Unsigned values
--use IEEE.NUMERIC_STD.ALL;

-- Uncomment the following library declaration if instantiating
-- any Xilinx leaf cells in this code.
--library UNISIM;
--use UNISIM.VComponents.all;

entity FA_tb is
--  Port ( );
end FA_tb;

architecture Behavioral of FA_tb is
component Full_adder_with_Half_adder is 
port (A,B,C : in std_logic;
        Sum, Carry : out std_logic);
        end component;
        signal A_tb,B_tb,C_tb,Sum_tb,Carry_tb : std_logic :='0';
begin
L1 : Full_adder_with_Half_adder port map (A_tb,B_tb,C_tb,Sum_tb,Carry_tb);
Stim_process: process
begin
wait for 50ns;
A_tb <= '0';B_tb <='0';C_tb <='0';wait for 50ns;
A_tb <= '0';B_tb <='0';C_tb <='1';wait for 50ns;
A_tb <= '0';B_tb <='1';C_tb <='0';wait for 50ns;
A_tb <= '0';B_tb <='1';C_tb <='1';wait for 50ns;
A_tb <= '1';B_tb <='0';C_tb <='0';wait for 50ns;
A_tb <= '1';B_tb <='0';C_tb <='1';wait for 50ns;
A_tb <= '1';B_tb <='1';C_tb <='0';wait for 50ns;
A_tb <= '1';B_tb <='1';C_tb <='1';wait for 50ns;
end process Stim_process;

end Behavioral;
```

