Construct a U shaped meander line. 
This VBA macro is used to construct a meander line, with ushaped alternating half cells. 
The current version constructs a line that extends along x direction only. For other directions, consider rotating the line.
The parameters and usage: 
mLine_Lu : length of the U arm
mLine_Ws : the gap between steps
mLine_Wt: trace width
mLine_xloc, mLine_yloc, mLine_zloc: coordinates of line start point. It is the center point of the trace. The line should have a thickness mt above this point.
mLine_Nu: number of U cells
mLine_L : required line extension
mLine_La : actual line extension
mLine_Lc : complementary flat length
mt       : metal thickness

Mehtodology: 
1. Import the .mcs file into CST
2. Extend the Parameters.json file in your CST/yourProject/Model with the given Parameters.json
3. Input the paramters' values suitable to your design
4. Run the Macro from Modelling Tab/VBA Macros
