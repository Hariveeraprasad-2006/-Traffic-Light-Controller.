# -Traffic-Light-Controller.
Project-Based-Experiment
# AIM:

To design and simulate the traffic light controller.

# SOFTWATE USED:

Quartus II

# THEORY:

 	Consider a controller for traffic at the intersection of three main roads.  
image
![image](https://github.com/Hariveeraprasad-2006/-Traffic-Light-Controller./assets/145049988/6bc4237e-a637-4c7e-bc47-df429bf77aec)


The traffic signal for all the three main roads have equal priority and they remain red by default.

In state 00,the traffic signals remains red for first five counts and yellow of road1 turns on for the next four counts.

In state 01, the green of road1 turns on for first five counts and yellow of road1 and road2 turns on for next four4 counts of this state.

In state 10, the traffic signal of road1 comes back to the red and that of road2 goes to green for tee first five counts.For the next four counts the traffic signal of road2 and road3 remains yellow.

In state 11, the traffic signal of road2 comes back to the red and that of road3 goes to green for the first five counts.For the next four counts the traffic signal of road3 turns to yellow

At the end of four states,the traffic signal of all the three roads come back to red.

# Task Assigned

From the HDL code given formulate the correct code  to divert the traffic to path 1 direction and disable the control in other directions (Assume user is at MR3 spot)

# Procedure

Type the program in Quartus software.
Compile and run the program.
Generate the RTL schematic and save the logic diagram.
Create nodes for inputs and outputs to generate the timing diagram.
For different input combinations generate the timing diagram
# Program:

# Program to implement the given logic function and to verify its operations in quartus using Verilog programming.
# Developed by: ARIKATLA HARI VEERA PRASAD
# RegisterNumber: 212223240014
```
module experiment (
    input clk,           // Clock input
    input reset,         // Reset input
    output reg road1_g, // Green signal for Road 1
    output reg road2_g, // Green signal for Road 2
    output reg road3_g, // Green signal for Road 3
    output reg road1_y, // Yellow signal for Road 1
    output reg road2_y, // Yellow signal for Road 2
    output reg road3_y  // Yellow signal for Road 3
);

// Define states
parameter [1:0] S_IDLE = 2'b00;
parameter [1:0] S_R1_G = 2'b01;
parameter [1:0] S_R2_G = 2'b10;
parameter [1:0] S_R3_G = 2'b11;

// Define state register
reg [1:0] state_reg;
reg [3:0] count_reg;

// Initial state
always @ (posedge clk or posedge reset)
begin
    if (reset)
    begin
        state_reg <= S_IDLE;
        count_reg <= 0;
    end
    else
    begin
        case(state_reg)
            S_IDLE: begin
                count_reg <= count_reg + 1;
                if (count_reg == 4'd4)
                begin
                    count_reg <= 0;
                    state_reg <= S_R1_G;
                end
            end
            S_R1_G: begin
                count_reg <= count_reg + 1;
                road1_g <= 1;
                road2_g <= 0;
                road3_g <= 0;
                if (count_reg == 4'd4)
                begin
                    count_reg <= 0;
                    state_reg <= S_R2_G;
                end
            end
            S_R2_G: begin
                count_reg <= count_reg + 1;
                road1_g <= 0;
                road2_g <= 1;
                road3_g <= 0;
                if (count_reg == 4'd4)
                begin
                    count_reg <= 0;
                    state_reg <= S_R3_G;
                end
            end
            S_R3_G: begin
                count_reg <= count_reg + 1;
                road1_g <= 0;
                road2_g <= 0;
                road3_g <= 1;
                if (count_reg == 4'd4)
                begin
                    count_reg <= 0;
                    state_reg <= S_IDLE;
                end
            end
        endcase
    end
end

// Yellow signals logic
always @ (posedge clk or posedge reset)
begin
    if (reset)
    begin
        road1_y <= 0;
        road2_y <= 0;
        road3_y <= 0;
    end
    else
    begin
        case(state_reg)
            S_IDLE: begin
                if (count_reg >= 4'd1 && count_reg <= 4'd4)
                    road1_y <= 1;
                else
                    road1_y <= 0;
            end
            S_R1_G, S_R2_G, S_R3_G: begin
                if (count_reg >= 4'd1 && count_reg <= 4'd4)
                begin
                    road1_y <= 1;
                    road2_y <= 1;
                    road3_y <= 1;
                end
                else
                begin
                    road1_y <= 0;
                    road2_y <= 0;
                    road3_y <= 0;
                end
            end
        endcase
    end
end

endmodule
```
# RTL Schematic
![image](https://github.com/Hariveeraprasad-2006/-Traffic-Light-Controller./assets/145049988/703998cf-2dc7-4d94-a5b1-c97bf4a47997)
# Result: 
Thus the design and simulate the traffic light controller are successfullt executed.
