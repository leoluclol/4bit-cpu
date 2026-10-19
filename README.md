# Custom 4-bit Harvard CPU Architecture in Digital

A custom-designed, Turing-complete 4-bit Harvard-style CPU architecture built entirely from scratch using the **Digital** logic simulator. This project bridges low-level hardware design (custom ALUs, microcoded Control Units, registers, and memory systems) with bare-metal assembly programming.

---

## 🚀 Key Architectural Features

* **Harvard Architecture:** Physically separated instruction memory (EEPROM) and data memory (RAM) to allow simultaneous instruction fetching and data access.
* **8-bit Instruction Word:** Formatted as `[4-bit Operand][4-bit Opcode]` (or vice-versa depending on control routing), executing one instruction per clock cycle for sequential instructions.
* **Custom 4-bit ALU:** Capable of parallel operations including Addition (via a 4-bit Adder with Carry-In support), Bitwise AND, OR, XOR, and software-driven subtraction via Two's Complement.
* **Microcoded Control Unit (ROM-based):** Uses a control ROM mapping opcodes to hardware control lines (Write Enables, Output Enables, and ALU selectors), eliminating messy combinational logic webs.
* **General Purpose Registers:** A bank of 4-bit registers (`4x4bit_Registers`) supporting flexible data routing and indirect memory addressing.
* **Control Flow:** Supports conditional and unconditional jumps (`JUMP`, `JPZ` - Jump if Zero) and execution halting (`HALT`).

---

## 🛠️ System Components & Datapath

1. **Program Counter (PC):** An 8-bit sequential register incremented by an internal 8-bit Adder (`PC + 1`) to fetch instructions from the EEPROM.
2. **EEPROM (Instruction Memory):** Stores the compiled hexadecimal machine code.
3. **RAM (Data Memory):** A dedicated data storage block allowing indirect read/write operations using register pointers.
4. **ALU Module:** Evaluates multiple logical/arithmetic channels simultaneously, routing the desired output via multiplexers based on control signals.
5. **Control Unit (`logic`):** Houses the instruction decoder ROM and routes immediate values/register selections across the internal bus.

---

## 📜 Custom Instruction Set Architecture (ISA)

| Name | Opcode (Hex/Bin) | Description |
| :--- | :--- | :--- |
| **NOOP** | `0x0` (`0000`) | No operation / Idle cycle. |
| **SET** | `0x1` (`0001`) | Load immediate value into target register. |
| **ADD** | `0x2` (`0010`) | Add registers and store result in destination. |
| **AND** | `0x3` (`0011`) | Bitwise AND between registers and store. |
| **OR** | `0x4` (`0100`) | Bitwise OR between registers and store. |
| **XOR** | `0x5` (`0101`) | Bitwise XOR between registers and store. |
| **STORE**| `0x6` (`0110`) | Store register value into RAM at an address held by a register. |
| **LOAD** | `0x7` (`0111`) | Load value from RAM into a register. |
| **JUMP** | `0x8` (`1000`) | Unconditional jump to target address. |
| **HALT** | `0x9` (`1001`) | Stop program execution. |
| **JPZ**  | `0xA` (`1010`) | Jump if Zero flag is active. |

---

## 📦 Getting Started & Simulation

1. **Prerequisites:** Download and install [HNeemann/Digital](https://github.com/HNeemann/Digital), an easy-to-use digital logic designer and simulator.
2. **Open the Project:** Load the main CPU schematic file into the simulator.
3. **Load Firmware:** 
   - Right-click the **EEPROM** component and paste your compiled hex program code.
   - Right-click the **RAM** component to initialize working memory values (e.g., input data for testing).
4. **Run Simulation:** Click the simulation **Play** button and step through the clock ticks to watch data flow across the bus lines and registers!

---

## 🧪 Example Test Program

An assembly test sequence running basic memory loads, arithmetic additions, and memory saves:

```text
17 37 22 65 86 00 00 00 00
```
*Loads data from RAM, performs arithmetic/logic operations, and writes the resulting output back to memory.*