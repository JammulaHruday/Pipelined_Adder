Pipelined 8-Input Adder Tree

Overview

A 3-stage pipelined adder tree designed to efficiently sum 8 unsigned 8-bit inputs.
Pipelining improves throughput by processing new inputs every clock cycle while previous additions are still in progress.
Fully simulated in Vivado and synthesizable for FPGA implementation.

Features

3 pipeline stages using DFFs for intermediate results.

Latency: 3 cycles, but new inputs accepted every clock.

Throughput improved vs. non-pipelined design.

Handles 8-bit overflow naturally (wrap-around).

Block Diagram

Stage 1 (8 → 4 Adders) → Stage 2 (4 → 2 Adders) → Stage 3 (Final Adder) in0,in1 ─► s0_reg ─┐ in2,in3 ─► s1_reg ─┤──► p0_reg ─┐ in4,in5 ─► s2_reg ─┤ ├─► final_sum_reg in6,in7 ─► s3_reg ─┘──► p1_reg ─┘ 

Simulation (Sample Results)

Time | s0 s1 s2 s3 | p0 p1 | Final -------------------------------------------- 15ns | 3 7 11 15 | 0 0 | 0 25ns | 30 70 110 150 | 10 26 | 0 45ns | 15 35 55 75 | 0 0 | 36 75ns | 254 254 254 254 | 252 252 | 180 85ns | 254 254 254 254 | 252 252 | 248 

Key Takeaways

Throughput ↑: new inputs every clock cycle.

Latency = 3 cycles due to pipelining.

Overflow handling via natural 8-bit wrap-around.
