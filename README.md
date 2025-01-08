# samsung-riscv


This repository contains an analysis of a simple RISC-V program that calculates the sum of numbers from 1 to \( n \). The analysis includes compiling the code, disassembling it, and debugging to examine register values during execution.  

---

## Task 1:  

The following is a screenshot of the compiled C program that calculates the sum of numbers from 1 to \( n \):  

![Compiled C Code Output - Oracle VirtualBox](https://github.com/user-attachments/assets/de80e2af-1786-43c6-be34-79d280125fe1)  

### Compilation Command  

The program was compiled using:  

```bash
riscv64-unknown-elf-gcc -Ofast -g -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
```  

- **`-Ofast`**: Enables aggressive optimizations for better performance.  
- **`-g`**: Includes debugging symbols in the compiled output.  
- **`-mabi=lp64`**: Specifies the LP64 ABI.  
- **`-march=rv64i`**: Targets the RISC-V 64-bit instruction set.  

### Objdump Output  

The disassembled output of the compiled binary file (`sum1ton.o`) was generated using the following command:  

```bash
riscv64-unknown-elf-objdump -d sum1ton.o | less
```  

Below is a screenshot of the output:  

![Objdump Output - Oracle VirtualBox](https://github.com/user-attachments/assets/78efaa37-336c-46be-9ab2-82e941eebf29)  

---
 Debugging and Register Analysis  

To debug the program and examine the register values, we used the following commands:  

```bash
spike -d pk sum1ton.o
until pc <address_of_main>
```  

- **`spike`**: Simulates the RISC-V processor.  
- **`-d`**: Enables debug mode for step-by-step execution.  
- **`pk`**: Runs the program under the proxy kernel.  
- **`until pc <address_of_main>`**: Steps through the program until the program counter reaches the `main` function.  

### Debugging Snapshots  

The following snapshots show the debugging process and register state at various stages of execution:  

1. **Initial Register State**:  
   ![Debugging Snapshot 1](https://github.com/user-attachments/assets/773cbdb7-9ec3-49ad-bba9-a74aa408d5fa)  

2. **Register Changes After Execution**:  
   ![Debugging Snapshot 2](https://github.com/user-attachments/assets/4bb931fd-43f0-47a3-be23-467315e1138c)  

3. **Program Counter and Stack Pointer**:  
   ![Debugging Snapshot 3](https://github.com/user-attachments/assets/2677fb1f-f721-487b-859d-64f9d12f6461)  

---

## Summary  

This repository demonstrates the process of compiling, disassembling, and debugging a RISC-V program. By using tools like `riscv64-unknown-elf-gcc`, `objdump`, and `spike`, we can gain valuable insights into the program's assembly-level instructions and runtime behavior.  

