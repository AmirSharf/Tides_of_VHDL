<div align = "center">
  <h1> Adder </h1>
  <sub> Author: <a> Amir Sharfuddin</a> <br>
    <small> Jan, 2022 </small>
  </sub> </div>
  
  --------

<img src = https://cdncontribute.geeksforgeeks.org/wp-content/uploads/1-77.png  class="center">

When we see above image three inputs (A,B,C-In) and two outputs(C-out,Sum ).
Lets take A and B is a 8 bits and C-In is set to 0's.

First define the `Source Code`
```JS
-- Define the library 
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;
use ieee.std_logic_unsigned.all;
use ieee.std_logic_arith.all;

-- Define the ports of the system
entity Adder_Design is
port ( A,B : in std_logic_vector ( 7 downto 0);
       Cin : in std_logic;
       Sum : out std_logic_vector (7 downto 0);
       Cout: out std_logic);
end Adder_Design;

-- Define the behiviour and functionality of the system
architecture Behavioral of Adder_Design is
signal x,y,z : std_logic_vector ( 8 downto 0);
begin
x <= '0' & A;
y <= '0' & B;
z <= x+y;
Sum <= z(7 downto 0);
Cout <= z(8);
end Behavioral;
```

After that it's necessary to define the `Testbench` of the system
```Js 
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;
use ieee.std_logic_unsigned.all;
use ieee.std_logic_arith.all;

entity Adder_tb is
--  Port ( );
end Adder_tb;

architecture Behavioral of Adder_tb is
component Adder_Design is
port ( A,B : in std_logic_vector ( 7 downto 0);
       Cin : in std_logic;
       Sum : out std_logic_vector (7 downto 0);
       Cout: out std_logic);
end component;
signal A_tb : std_logic_vector(7 downto 0);
signal B_tb : std_logic_vector(7 downto 0);
signal Cin_tb : std_logic;
signal Sum_tb : std_logic_vector(7 downto 0);
signal Cout_tb : std_logic;
begin
L1 : Adder_Design port map (A_tb,B_tb,Cin_tb,Sum_tb,Cout_tb);
stim_process : process
begin
wait for 20ns;
A_tb <= "00000000";
B_tb <= "00000000";
wait for 20ns;

A_tb <= "00000000";
B_tb <= "00010000";
wait for 20ns;
A_tb <= "00000000";
B_tb <= "10101010";
wait for 20ns;
A_tb <= "00000000";
B_tb <= "01010000";
wait for 20ns;
A_tb <= "00000000";
B_tb <= "01111111";
wait for 20ns;
A_tb <= "00000000";
B_tb <= "11110100";
wait for 20ns;
A_tb <= "00000000";
B_tb <= "11111000";
wait for 20ns;
A_tb <= "00000000";
B_tb <= "11111100";
wait for 20ns;
A_tb <= "00000000";
B_tb <= "11111101";
wait for 20ns;
A_tb <= "00000000";
B_tb <= "11111110";
wait for 20ns;
A_tb <= "00000000";
B_tb <= "11111111";
end process stim_process;
end Behavioral;
```
After that click on the Simulation > Run Simulation > Run Behavioral Simulation <br>
As you can see in the below that 
![image](https://user-images.githubusercontent.com/71962033/152110618-7b48c1ab-6e59-49cc-94e5-787d7a5ecec0.png)

That's all from my side of Adder 
