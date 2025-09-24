# EXPERIMENT 3B: Simulation of All Flip-Flops using Non Blocking Statement

## AIM
To design and simulate basic flip-flops (SR, D, JK, and T) using **Non blocking statements** in Verilog HDL, and verify their functionality through simulation in Vivado 2023.1.

## APPARATUS REQUIRED
- Vivado 2023.1
- Computer with HDL Simulator

## DESCRIPTION
Flip-flops are the basic memory elements in sequential circuits.  
In this experiment, different types of flip-flops (SR, D, JK, T) are modeled using **behavioral modeling** with **Non blocking assignment (`<=`)** inside the `always` block.  
Non Blocking assignments execute sequentially in the given order, which makes it easier to describe simple synchronous circuits.

## PROCEDURE
1. Open **Vivado 2023.1**.  
2. Create a **New RTL Project** (e.g., `FlipFlop_Simulation`).  
3. Add Verilog source files for each flip-flop (SR, D, JK, T).  
4. Add a testbench file to verify all flip-flops.  
5. Run **Behavioral Simulation**.  
6. Observe waveforms of inputs and outputs for each flip-flop.  
7. Verify that outputs match the truth table.  
8. Save results and capture simulation screenshots.

---

## VERILOG CODE

### SR Flip-Flop (Non Blocking)
```verilog
module sr_ff(S, R, clk, rst, Q);
    input S, R, clk, rst;
    output reg Q;

    always @(posedge clk) begin
        if (rst == 1) 
            Q <= 1'b0;        
        else if (S == 0 && R == 0) 
            Q <= Q;            
        else if (S == 0 && R == 1) 
            Q <= 1'b0;         
        else if (S == 1 && R == 0) 
            Q <= 1'b1;         
        else 
            Q <= 1'bx;       
    end
endmodule
```
### SR Flip-Flop Test bench 
```verilog
`timescale 1ns / 1ps
module tb_sr_ff;
    reg S, R, clk, rst;
    wire Q;

    sr_ff uut(S, R, clk, rst, Q);

    always #5 clk = ~clk;  

    initial begin
        clk = 0; S = 0; R = 0; rst = 1;
        #10 rst = 0;
        #10 S = 1; R = 0;
        #10 S = 0; R = 0;
        #10 S = 0; R = 1;
        #10 S = 1; R = 1;
        #10 S = 0; R = 0;
        #20 $finish;
    end
endmodule

```
#### SIMULATION OUTPUT

![image](https://github.com/user-attachments/assets/903a8a02-4ffc-4419-b6fe-19873f51cfae)

---

### JK Flip-Flop (Non Blocking)
```verilog
module jk_ff(J,K,clk,rst,Q);
input J,K,clk,rst;
output reg Q;
always @(posedge clk)
begin
if (rst==1) Q<=1'b0;
else if  (J==0 && K==0) 
Q<=Q;
else if (J==0 && K==1) 
Q<=1'b0;
else if (J==1 && K==0) 
Q<=1'b1;
else 
Q<= ~Q;
end
endmodule
```
### JK Flip-Flop Test bench 
```verilog
`timescale 1ns / 1ps
module tb_jk_ff;
reg J,K,clk,rst;
wire Q;
jk_ff uut(J,K,clk,rst,Q);
always #5 clk=~clk;
initial begin
clk=0; J=0; K=0; rst=1;
#10 rst=0;
#10 J=1; K=0;
#10 J=0; K=0;
#10 J=0; K=1;
#10 J=1; K=1;
#10 J=0; K=0;
#20 $finish;
end
endmodule
```
#### SIMULATION OUTPUT

![image](https://github.com/user-attachments/assets/15f22cef-d440-48ef-84fc-85e062f59df2)


---
### D Flip-Flop (Non Blocking)
```verilog
module d_ff(clk,rst,D,Q);
input clk,rst,D;
output reg Q;
always @ (posedge clk)
begin
if (rst==1)
Q<=0;
else 
Q<=Q;
end
endmodule

```
### D Flip-Flop Test bench 
```verilog

`timescale 1ns / 1ps
module d_tb_ff;
reg clk,rst,D;
wire Q;
d_ff uut (clk,rst,D,Q);
always #5 clk=~clk;
initial
begin
clk=0; D=0; rst=1;
#10 rst=0;
D=Q;
$finish;
end
endmodule

```

#### SIMULATION OUTPUT

![image](https://github.com/user-attachments/assets/841171e5-165f-4908-bc24-886e9a578ab2)

---
### T Flip-Flop (Non Blocking)
```verilog

module t_ff(clk,rst,T,Q);
input clk,rst,T;
output reg Q;
always @ (posedge clk)
begin
if (rst==1)
Q<=0;
else if (T==0)
Q<=Q;
else 
Q<=~Q;
end
endmodule
```
### T Flip-Flop Test bench 
```verilog
`timescale 1ns / 1ps

module t_tb_ff;
reg clk,rst,T;
wire Q;
t_ff uut (clk,rst,T,Q);
always #5 clk=~clk;
initial
begin
clk=0; T=0; rst=1;
#10 rst=0;
T=0;
#10 T=1;
$finish;
end
endmodule

```

#### SIMULATION OUTPUT

![image](https://github.com/user-attachments/assets/c7dbe488-4e99-49fd-a471-2fb3d1d1dfed)

---

### RESULT

All flip-flops (SR, D, JK, T) were successfully simulated using Non blocking statements in Verilog HDL.
The outputs matched the expected truth table values, demonstrating correct sequential behavior.
