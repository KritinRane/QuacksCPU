# QuacksCPU 🦆

A simple single-cycle processor designed and simulated in **Logisim Evolution**, built as part of CS 382 at Stevens Institute of Technology. Includes a custom Python assembler that compiles human-readable assembly into hex image files loadable directly into the CPU's instruction memory.

---

## Architecture

The CPU contains **4 general-purpose registers** (x0–x3) and **2 RAM modules** (instruction memory and data memory).

### Supported Operations
- Addition (`ADD`)
- Subtraction (`SUB`)
- Load from memory (`LDR`)
- Store to memory (`STR`)

### Operand Types
Each instruction supports two operand modes, selected via a **mode bit (M)**:
- `M = 0` → Immediate operand
- `M = 1` → Register operand

---

## Instruction Set

| Instruction | Opcode | Format |
|-------------|--------|--------|
| ADD | `00` | `ADD Rt Rn Rm/IMM` |
| SUB | `01` | `SUB Rt Rn Rm/IMM` |
| LDR | `10` | `LDR Rt Rn Rm/IMM` |
| STR | `11` | `STR Rt Rn Rm/IMM` |

### Instruction Format
```
ADD: | 00 | M | Operand[7:0] | Rd | Rs |
SUB: | 01 | M | Operand[7:0] | Rd | Rs |
LDR: | 10 | M | Operand[7:0] | Rd | Rs |
STR: | 11 | M | Operand[7:0] | Rd | Rs |
```

---

## Setup & Usage

### 1. Assemble the program
Place `simulation.py` and `simulation.txt` in the same folder, then run:
```bash
python3 simulation.py
```
This generates two files:
- `instruction_mem_img` — load into Instruction Memory
- `data_mem_img` — load into Data Memory

> Note: Instructions in `simulation.txt` are **case sensitive**.

### 2. Load into Logisim
1. Open `JITerry.circ` in Logisim Evolution
2. Right-click **Instruction Memory** → Load Image → select `instruction_mem_img`
3. Right-click **Data Memory** → Load Image → select `data_mem_img`

### 3. Run the simulation
Cycle through instructions using the clock. When the **PC hits 6**, inspect the register file to verify output values.

---

## Assembly Syntax
```
ADD Rd Rn Rm    # Rd = Rn + Rm
SUB Rd Rn Rm    # Rd = Rn - Rm
LDR Rd Rn Rm    # Rd = Mem[Rn + Rm]
STR Rt Rn Rm    # Mem[Rn + Rm] = Rt
```
Immediate values can replace `Rm` in any instruction.

---

## Files
| File | Description |
|------|-------------|
| `JITerry.circ` | Logisim Evolution circuit file |
| `simulation.py` | Python assembler — compiles `.txt` assembly to hex images |
| `simulation.txt` | Sample assembly program |

---

## Tech Stack
- **Logisim Evolution** — circuit design and simulation
- **Python 3** — custom assembler

---

*Built by Kritin Rane — Computer Science, Stevens Institute of Technology*  
*I pledge my honor that I have abided by the Stevens Honor System.*
