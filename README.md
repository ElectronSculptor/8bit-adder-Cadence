# ASIC Design – 8-bit Adder using Cadence Virtuoso (AMS 0.35µm)

This project focuses on the **schematic design, simulation, and timing analysis** of an **8-bit ripple-carry adder**, designed and verified using **Cadence Virtuoso** and the **AMS 0.35µm (C35B4)** technology.  
It was carried out as part of an **ASIC design lab** at the *École des Mines de Saint-Étienne (ISMIN)* by **Gevorg Ishkhanyan** and **Bilel Betka**.

---

## 📘 Objectives
- Design an **8-bit adder** hierarchically using CMOS logic gates.  
- Simulate and verify each subcircuit step by step (Half Adder → Full Adder → 8-bit Adder).  
- Validate the logical behavior through **transient simulations** in **Cadence ADE XL**.  
- Identify and analyze the **critical path** to evaluate propagation delays.  

---

## ⚙️ Tools & Technology
- **Software**: Cadence Virtuoso, ADE XL  
- **Technology**: AMS 0.35µm (C35B4)  
- **Logic gates used**: NAND-based synthesis (`CORELIB/nand20`)

---

## 🧩 Hierarchical Design Approach

The project follows a **bottom-up design methodology**:
1. Design and verify the **Half Adder**
2. Use it to build and test a **Full Adder**
3. Cascade eight Full Adders to create an **8-bit Ripple-Carry Adder**

---

## 🔹 Half Adder

The Half Adder adds two bits **A** and **B**, producing:
- Sum: $S = A \oplus B$
- Carry: $C = A \cdot B$

It was implemented using **only NAND gates**, applying De Morgan’s laws.

<p align="center">
  <img src="./half_adder/Cellview%20halfadder.png" alt="Half Adder schematic" width="350"/>
  <img src="./half_adder/cellview%20testbench%20halfadder.png" alt="Half Adder testbench" width="350"/>
</p>

**Transient Simulation:**
<p align="center">
  <img src="./half_adder/chronogramme%20testbench%20halfadder.png" alt="Half Adder waveform" width="600"/>
</p>

✅ The simulation results confirm the expected truth table behavior.

---

## 🔸 Full Adder

The Full Adder adds **A**, **B**, and **Cin**, and outputs:
- Sum: $S = (A \oplus B) \oplus C_{in}$  
- Carry: $C_{out} = (A \cdot B) + (C_{in} \cdot (A \oplus B))$  

The design reuses **two Half Adders** and one **NAND-based carry circuit**.

<p align="center">
  <img src="./full_adder/Cellview%20Fulladder.png" alt="Full Adder schematic" width="550"/>
  <img src="./full_adder/cellview%20testbench%20fulladder.png" alt="Full Adder testbench" width="350"/>
</p>

**Simulation Result:**
<p align="center">
  <img src="./full_adder/Chronogramme%20testbench%20fulladder.png" alt="Full Adder waveform" width="600"/>
</p>

✅ Simulation verifies that both **Sum** and **Cout** match the truth table.

---

## 🧠 8-bit Ripple-Carry Adder

The 8-bit adder was built using **8 Full Adders in cascade**.  
Each stage propagates the carry to the next one, forming a **ripple-carry structure**.

<p align="center">
  <img src="./adder_8bit/schematic%208bit.png" alt="8-bit Adder schematic" width="450"/>
  <img src="./adder_8bit/schematic%208bit%20testbench.png" alt="8-bit Adder testbench" width="450"/>
</p>

**Analog Simulation (Transient):**
<p align="center">
  <img src="./adder_8bit/chronogramme%20propagation.png" alt="8-bit Adder analog waveform" width="600"/>
</p>

**Digital View (Hexadecimal Output):**
<p align="center">
  <img src="./adder_8bit/chronogramme%20digital.png" alt="8-bit Adder digital waveform" width="600"/>
</p>

✅ The 8-bit adder correctly computes the sum for all tested input combinations.

---

## 🕒 Critical Path Analysis

The **critical path** determines the maximum propagation delay of the circuit.

| Circuit | Output | Delay Expression | Equivalent Delay |
|----------|---------|------------------|------------------|
| Half Adder | S | $\delta_{HA}(S) = 3\delta$ | 3δ |
| Full Adder | Cout | $\delta_{FA}(C_{out}) = 5\delta$ | 5δ |
| 8-bit Adder | Cout | $\delta_{8A}(C_{out}) = 19\delta$ | 19δ |

Thus, the total delay of the 8-bit adder is approximately **19 gate delays (19δ)**, corresponding to the propagation of the carry through all stages.

---

## 🧮 Observations
- The hierarchical design simplifies debugging and reuse.  
- The ripple-carry structure, while simple, introduces a **long delay** due to serial carry propagation. 

---

## ✅ Conclusion
- Designed and simulated an **8-bit ripple-carry adder** in Cadence Virtuoso using AMS 0.35µm technology.  
- Verified logical correctness through hierarchical simulations.  
- Analyzed the **critical path** and propagation delays.  
- The final design can be used as a base block for future **digital ASIC implementations**.

---
