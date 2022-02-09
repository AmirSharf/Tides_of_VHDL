_ Don't follow the code yet. It's under verification_
<br>
<br>
`Source Code`
```JS
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;
use ieee.std_logic_arith.all;
use ieee.std_logic_unsigned.all;

-- Uncomment the following library declaration if using
-- arithmetic functions with Signed or Unsigned values
--use IEEE.NUMERIC_STD.ALL;

-- Uncomment the following library declaration if instantiating
-- any Xilinx leaf cells in this code.
--library UNISIM;
--use UNISIM.VComponents.all;

entity ALU is
port (a,b : in std_logic_vector (7 downto 0);
        sel : in std_logic_vector (3 downto 0);
        cin : in std_logic;
         y : out std_logic_vector (7 downto 0));
end ALU;

architecture Behavioral of ALU is
signal logical, arith : std_logic_vector (7 downto 0 ); 
begin
with sel(2 downto 0) select
logical <= not a when "000",
           not b when "001",
           a and b when "010",
           a or b when "011",
           a nand b when "100",
           a nor b when "101",
           a xor b when "110",
           a xnor b when "111";
           when others => y<="Z";
      
 with sel(2 downto 0) select
 arith <= a when "000",
          b when "001",
          a-1 when "010",
          b-1 when "011",
          a+1 when "100",
          b+1 when "101",
          a+b when "110",
          a+b+cin when "111";
          

  y <= logical when  sel(3)='0' else
      arith when sel(3)='1';
           
end Behavioral;
```

`Test Bench`
```css
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity ALU_tb is
--  Port ( );
end ALU_tb;

architecture Behavioral of ALU_tb is
component ALU is
port (a,b : in std_logic_vector (7 downto 0);
        sel : in std_logic_vector (3 downto 0);
        cin : in std_logic;
         y : out std_logic_vector (7 downto 0));
         
signal (a_tb, b_tb : std_logic_vector( 7 downto 0) := (others=>'0');
        cin_tb : std_logic;
        sel_tb : std_logic_vector(3 downto 0));
begin
l1 : ALU ( port map a_tb , b_tb, cin_tb, sel_tb,y_tb);
a_tb <= "00000000" after 80ns, "00000001" after 160ns;
b_tb <= "00000000" after 80ns, "00111111" after 160ns;
sel <= "0000";
for i in 0 to 10 loop
sel <= sel + "0001";
wait for 80ns;
end loop

end Behavioral;
```
`Waveform`
![image](https://user-images.githubusercontent.com/71962033/152400941-fb612df4-b425-4d0b-b451-45f295da3020.png)

<pre>

</pre>
