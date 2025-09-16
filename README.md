# ⚡ Pipelined 8-Input Adder Tree  

---

## 📌 Project Overview  

This project implements a *3-stage pipelined adder tree* to sum *8 unsigned 8-bit inputs efficiently*.  
Pipelining improves *throughput* by processing new inputs every clock cycle, even while previous additions are still being computed.  

✅ The final design *simulates successfully in Vivado* and is *fully synthesizable for FPGA implementation*.  

---

## 🎯 Objective  

- *Without Pipelining* → The next set of inputs must wait until the entire addition finishes.  
- *With Pipelining* → New inputs can be processed *every clock cycle*, increasing throughput.  

---

##  Block Diagram (Pipeline Stages)

### Stage 1 → Pairwise Adders (8 inputs → 4 sums)
 in0 ─┐       in2 ─┐       in4 ─┐       in6 ─┐
      ├─►[ + ]     ├─►[ + ]     ├─►[ + ]     ├─►[ + ]
 in1 ─┘       in3 ─┘       in5 ─┘       in7 ─┘
      │           │           │           │
     s0          s1          s2          s3
      │           │           │           │
     [DFF]       [DFF]       [DFF]       [DFF]

---

### Stage 2 → Partial Sum Adders (4 sums → 2 sums)
 s0_reg ─┐                   s2_reg ─┐
         ├─►[ + ]             ├─►[ + ]
 s1_reg ─┘                   s3_reg ─┘
         │                     │
        p0                    p1
         │                     │
        [DFF]                 [DFF]

---

### Stage 3 → Final Adder (2 sums → Final Result)
 p0_reg ─┐
         ├─►[ + ]──► final_sum
 p1_reg ─┘
         │
       [DFF]
         │
  final_sum_reg

💡 DFFs (pipeline registers) store intermediate results between stages, allowing new inputs every clock cycle.  

---

## 🖥 Simulation Results  

*Vivado Behavioral Simulation Console Output:*  

===========================================================  
 Pipelined 8-Input Adder Tree Simulation (CLEAN TEST CASES)  
===========================================================  
Time | s0  s1  s2  s3 | p0   p1  | Final  
-----------------------------------------------------------  
  0ns |   0   0   0   0 |   0    0 |   0  
 15ns |   3   7  11  15 |   0    0 |   0  
 25ns |  30  70 110 150 |  10   26 |   0  
 35ns |   0   0   0   0 | 100    4 |   0  
 45ns |  15  35  55  75 |   0    0 |  36  
 55ns | 254 254 254 254 |  50  130 | 104  
 65ns | 254 254 254 254 | 252  252 |   0  
 75ns | 254 254 254 254 | 252  252 | 180  
 85ns | 254 254 254 254 | 252  252 | 248  
-----------------------------------------------------------  
Simulation Completed ✅  

---

## 🔑 Key Learnings  

- 🚀 *Throughput Improvement* → Pipelining allows overlapping computations.  
- 📝 *Pipeline Registers (DFFs)* → Store intermediate sums at each stage.  
- ⏱ *Latency* → The final sum is available after *3 clock cycles*, but new inputs can still enter every cycle.  
- 🔄 *Overflow Handling* → Wraps naturally due to 8-bit arithmetic.  

---

## 📂 Tools Used  

- *Xilinx Vivado 2025.1* → Design, simulation, and synthesis  
- *Verilog HDL* → RTL implementation  
- *FPGA* → Target hardware platform  

---
