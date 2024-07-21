`timescale 1ns / 1ps
//////////////////////////////////////////////////////////////////////////////////
// Company: 
// Engineer: 
// 
// Create Date: 07/17/2024 06:44:08 PM
// Design Name: 
// Module Name: nbitadd
// Project Name: 
// Target Devices: 
// Tool Versions: 
// Description: 
// 
// Dependencies: 
// 
// Revision:
// Revision 0.01 - File Created
// Additional Comments:
// 
//////////////////////////////////////////////////////////////////////////////////


module N_bit_adder(input1,input2,answer,carry_out);
parameter N=32;
input [N-1:0] input1,input2;
   output reg [N-1:0] answer;
   output   carry_out;
  wire [N-1:0] carry;
   genvar i;
   generate 
 // integer i;
  //always@(input1 or input2)
  //begin
   for(i=0;i<N;i=i+1)
     begin:genrated_block
   if(i==0) 
  half_adder f(input1[0],input2[0],answer[0],carry[0]);
   else
  full_adder f2(input1[i],input2[i],carry[i-1],answer[i],carry[i]);
     end
  assign carry_out = carry[N-1];
 // end
   endgenerate
endmodule 

module half_adder(x,y,s,c);
   input x,y;
   output s,c;
   assign s=x^y;
   assign c=x&y;
endmodule 
//for full adder 
module full_adder(x,y,c_in,s,c_out);
   input x,y,c_in;
   output s,c_out;
 assign s = (x^y) ^ c_in;
 assign c_out = (y&c_in)| (x&y) | (x&c_in);
endmodule 
