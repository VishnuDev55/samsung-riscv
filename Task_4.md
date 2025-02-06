![b  Running  - Oracle VirtualBox 08-01-2025 9 28 32 PM](https://github.com/user-attachments/assets/108b5b0c-a1f7-4bc5-93d2-ba1130cbfb70)
### Basics of Observing Waveforms in GTKWave for RISC-V Simulation

GTKWave is a waveform viewer used to analyze signals from your Verilog simulation. Here's a basic guide to what you can observe:

#### Key Signals to Monitor

1. **Clock Signal (`clk`)**
   - **Purpose:** Synchronizes all sequential operations.
   - **Behavior:** A square wave toggling between `1` and `0`.

2. **Reset Signal (`RN`)**
   - **Purpose:** Initializes the system.
   - **Behavior:** Active (`1`) during reset and inactive (`0`) after a few cycles.

3. **Program Counter (`NPC`)**
   - **Purpose:** Tracks the address of the next instruction.
   - **Behavior:** Increments sequentially or jumps for branch instructions.

4. **Write-Back Output (`WB_OUT`)**
   - **Purpose:** Holds the result of executed instructions.
   - **Behavior:** Displays results from operations like addition, subtraction, or memory access.

5. **Pipeline Signals**
   - **Examples:** Instruction fetch (`IF_ID_IR`), operands (`ID_EX_A`, `ID_EX_B`), ALU output (`EX_MEM_ALUOUT`), and memory data (`MEM_WB_LDM`).
   - **Purpose:** Trace data movement through the pipeline stages.

6. **Branch Enable (`BR_EN`)**
   - **Purpose:** Indicates whether a branch condition is met.
   - **Behavior:** `1` if the condition is satisfied, `0` otherwise.

#### Steps to Use GTKWave

1. Run your simulation to generate the `.vcd` (Value Change Dump) file.
2. Open GTKWave:
   ```bash
   gtkwave <filename>.vcd
   ```
3. Add signals of interest to the waveform viewer.
4. Analyze the signal behavior over time to verify your design.

#### Use Cases

- Debug clock and reset functionality.
- Verify program flow through the program counter.
- Ensure correct execution of instructions by checking the write-back stage.
- Trace issues in the pipeline or branch logic using intermediate signals.

This basic understanding will help you effectively debug and validate your RISC-V processor design.
