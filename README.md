# Pipelined 8-Input Adder Tree  

---

##  Project Overview  

This project implements a **3-stage pipelined adder tree** to efficiently sum **8 unsigned 8-bit inputs**.  
Pipelining improves **throughput** by allowing new inputs to be processed every clock cycle, even while previous additions are still in progress.  

The final design **simulates successfully in Vivado** and is **fully synthesizable for FPGA implementation**.  

---

##  Objective  

- **Without Pipelining** → The next set of inputs must wait until the *entire addition* completes.  
- **With Pipelining** → New inputs can be processed **every clock cycle**, greatly improving throughput.  

---

## 🏗 Block Diagram (Pipeline Stages)  

### **Stage 1 → Pairwise Adders (8 inputs → 4 sums)**  

| Input Pair | Operation | Output | Register |
|------------|-----------|--------|----------|
| `in0 + in1` | ➝ | `s0` | → `[DFF] → s0_reg` |
| `in2 + in3` | ➝ | `s1` | → `[DFF] → s1_reg` |
| `in4 + in5` | ➝ | `s2` | → `[DFF] → s2_reg` |
| `in6 + in7` | ➝ | `s3` | → `[DFF] → s3_reg` |

---

### **Stage 2 → Partial Sum Adders (4 sums → 2 sums)**  

| Input Pair | Operation | Output | Register |
|------------|-----------|--------|----------|
| `s0_reg + s1_reg` | ➝ | `p0` | → `[DFF] → p0_reg` |
| `s2_reg + s3_reg` | ➝ | `p1` | → `[DFF] → p1_reg` |

---

### **Stage 3 → Final Adder (2 sums → Final Result)**  

| Input Pair | Operation | Output | Register |
|------------|-----------|--------|----------|
| `p0_reg + p1_reg` | ➝ | `final_sum` | → `[DFF] → final_sum_reg` |

💡 **Note:** DFFs (pipeline registers) store intermediate results between stages, enabling **new inputs every cycle**.  

---

## 🖥 Simulation Results  

### Pipelined 8-Input Adder Tree Simulation (CLEAN TEST CASES)  

| Time |   s0 |   s1 |   s2 |   s3 |  p0 |  p1 | Final |
|------|-----:|-----:|-----:|-----:|----:|----:|------:|
|  0ns |    0 |    0 |    0 |    0 |   0 |   0 |     0 |
| 15ns |    3 |    7 |   11 |   15 |   0 |   0 |     0 |
| 25ns |   30 |   70 |  110 |  150 |  10 |  26 |     0 |
| 35ns |    0 |    0 |    0 |    0 | 100 |   4 |     0 |
| 45ns |   15 |   35 |   55 |   75 |   0 |   0 |    36 |
| 55ns |  254 |  254 |  254 |  254 |  50 | 130 |   104 |
| 65ns |  254 |  254 |  254 |  254 | 252 | 252 |     0 |
| 75ns |  254 |  254 |  254 |  254 | 252 | 252 |   180 |
| 85ns |  254 |  254 |  254 |  254 | 252 | 252 |   248 |

✅ **Simulation Completed Successfully**  

---

## 🔑 Key Learnings  

- 🚀 **Throughput Improvement** → Pipelining allows overlapping computations.  
- 📝 **Pipeline Registers (DFFs)** → Store intermediate sums at each stage.  
- ⏱ **Latency** → The final sum appears after **3 clock cycles**, but new inputs can still be entered every cycle.  
- 🔄 **Overflow Handling** → Natural wrap-around due to 8-bit arithmetic.  

---

## 📂 Tools Used  

- **Xilinx Vivado 2025.1** → Design, simulation, and synthesis  
- **Verilog HDL** → RTL implementation  
- **FPGA** → Target hardware platform  

---
