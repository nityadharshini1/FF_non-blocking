# FF_blocking_non-blocking
# EXPERIMENT 3A: Simulation of All Flip-Flops using Blocking Statement
# AIM
To design and simulate basic flip-flops (SR, D, JK, and T) using blocking statements in Verilog HDL, and verify their functionality through simulation in Vivado 2023.1.

# APPARATUS REQUIRED
Vivado 2023.1
Computer with HDL Simulator
# DESCRIPTION
Flip-flops are the basic memory elements in sequential circuits.
In this experiment, different types of flip-flops (SR, D, JK, T) are modeled using behavioral modeling with blocking assignment (=) inside the always block.
Blocking assignments execute sequentially in the given order, which makes it easier to describe simple synchronous circuits.

# PROCEDURE
Open Vivado 2023.1.
Create a New RTL Project (e.g., FlipFlop_Simulation).
Add Verilog source files for each flip-flop (SR, D, JK, T).
Add a testbench file to verify all flip-flops.
Run Behavioral Simulation.
Observe waveforms of inputs and outputs for each flip-flop.
Verify that outputs match the truth table.
Save results and capture simulation screenshots.
# VERILOG CODE

SR Flip-Flop (Non-Blocking)

module sr_ff(S, R, clk, rst, Q);
    input S, R, clk, rst;
    output reg Q;

    always @(posedge clk)
    begin
        if (rst == 1)
            Q <= 0;
        else
        begin
            case ({S, R})
                2'b00: Q <= Q;
                2'b01: Q <= 1'b0;
                2'b10: Q <= 1'b1;
                2'b11: Q <= 1'bX;
            endcase
        end
    end

endmodule



SR Flip-Flop Testbench

module sr_ff_tb;
    reg S, R, clk, rst;
    wire Q;

    sr_ff uut(S, R, clk, rst, Q);

    initial
    begin
        clk = 0;
        S = 0;
        R = 0;
        rst = 1;

        #10 rst = 0;
        #10 S = 0; R = 0;
        #10 S = 0; R = 1;
        #10 S = 1; R = 0;
        #10 S = 1; R = 1;

        #10 $finish;
    end

    always #5 clk = ~clk;

endmodule

SIMULATION OUTPUT 
![WhatsApp Image 2026-03-19 at 3 51 30 PM](https://github.com/user-attachments/assets/d8b10bcb-e0ef-4252-bad3-b3ef71e80287)




JK Flip-Flop (Non-Blocking)

module jk_ff(J, K, clk, rst, Q);
    input J, K, clk, rst;
    output reg Q;

    always @(posedge clk)
    begin
        if (rst == 0)
            Q <= 0;
        else
        begin
            case ({J, K})
                2'b00: Q <= Q;
                2'b01: Q <= 1'b0;
                2'b10: Q <= 1'b1;
                2'b11: Q <= ~Q;   // Toggle condition
            endcase
        end
    end

endmodule


JK Flip-Flop Testbench

module jk_ff_tb;
    reg J, K, clk, rst;
    wire Q;

    jk_ff uut (J, K, clk, rst, Q);

    initial 
    begin  
        clk = 0;
        rst = 0;   // Apply reset first
        J = 0;
        K = 0;

        #10 rst = 1;   // Release reset

        #10 J = 0; K = 0;
        #10 J = 0; K = 1;
        #10 J = 1; K = 0;
        #10 J = 1; K = 1;

        #10 $finish;
    end

    always #5 clk = ~clk;

endmodule


SIMULATION OUTPUT
![WhatsApp Image 2026-03-19 at 3 57 00 PM](https://github.com/user-attachments/assets/1655b831-c44c-478a-9c78-1964c12efc03)




D Flip-Flop (Non-Blocking)

module d_ff(D, clk, rst, Q);
    input D, clk, rst;
    output reg Q;

    always @(posedge clk)
    begin
        if (rst == 1)
            Q <= 0;
        else
            Q <= D;
    end

endmodule


D Flip-Flop Testbench

module d_ff_tb;
    reg D, rst, clk;
    wire Q;

    d_ff uut(D, clk, rst, Q);

    initial
    begin
        clk = 0;
        rst = 1;   // Apply reset
        D = 0;

        #10 rst = 0;   // Release reset

        #10 D = 0;
        #10 D = 1;

        #20 $finish;
    end

    always #5 clk = ~clk;

endmodule

SIMULATION OUTPUT

![WhatsApp Image 2026-03-19 at 4 00 00 PM](https://github.com/user-attachments/assets/92b8d567-ad5a-4c75-90b6-f323adf99e7d)


T Flip-Flop (Non-Blocking)

module t_ff(T, clk, rst, Q);
    input T, clk, rst;
    output reg Q;

    always @(posedge clk)
    begin
        if (rst == 1)
            Q <= 0;
        else if (T == 0)
            Q <= Q;
        else
            Q <= ~Q;
    end

endmodule


T Flip-Flop Testbench

module t_ff_tb;
    reg T, rst, clk;
    wire Q;

    t_ff uut(T, clk, rst, Q);

    initial
    begin
        clk = 0;
        rst = 1;   // Apply reset
        T = 0;

        #10 rst = 0;   // Release reset

        #10 T = 0;
        #10 T = 1;

        #10 $finish;
    end

    always #5 clk = ~clk;

endmodule

SIMULATION OUTPUT

![WhatsApp Image 2026-03-19 at 4 03 12 PM](https://github.com/user-attachments/assets/54fc5fc5-5e3b-4a15-b09d-1614d0a2d251)

# RESULT
All flip-flops (SR, D, JK, T) were successfully simulated using Non blocking statements in Verilog HDL. The outputs matched the expected truth table values, demonstrating correct sequential behavior.
