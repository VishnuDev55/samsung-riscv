## **Designing a Full Adder Using VSDSquadron Mini**

### **Project Summary**
This project demonstrates the implementation of a Full Adder circuit, a fundamental building block in digital electronics, using the VSDSquadron Mini development platform based on RISC-V architecture. The Full Adder takes in two binary digits and a carry-in input, producing a sum and carry-out output. This design is crucial for creating more complex arithmetic circuits in digital systems. The goal of this project is to apply digital logic principles, integrate them with RISC-V systems, and showcase the implementation by utilizing GPIO pins for reading inputs and displaying results via LEDs. The project is developed and simulated through the PlatformIO IDE.

### **Components Required**
- **VSDSquadron Mini Development Board**
- **Push Buttons** for binary input
- **2 LEDs** for sum and carry output visualization
- **Breadboard** for connecting components
- **Jumper Wires** to establish connections
- **VS Code** with PlatformIO extension for coding and simulation

### **Hardware Configuration**
- **Inputs:** Three single-bit inputs (A, B, Cin) connected to the GPIO pins on VSDSquadron Mini via push buttons placed on the breadboard.
- **Outputs:** Two LEDs (Sum and Carry) connected to display the calculated result of the Full Adder.
- **GPIO Pin Setup:** Configured as per the official reference manual for proper interaction between the components.

![Full Adder on VSDSquadron Mini](https://github.com/maazm007/vsdsquadron-mini-internship/assets/83294849/e91fafca-c9ff-4acc-b6c2-0d6028944f82)

### **Truth Table for Full Adder**
| **A** | **B** | **Cin** | **Sum** | **Carry** |
| :---: | :---: | :-----: | :-----: | :-------: |
|   0   |   0   |    0    |    0    |     0     |
|   0   |   0   |    1    |    1    |     0     |
|   0   |   1   |    0    |    1    |     0     |
|   0   |   1   |    1    |    0    |     1     |
|   1   |   0   |    0    |    1    |     0     |
|   1   |   0   |    1    |    0    |     1     |
|   1   |   1   |    0    |    0    |     1     |
|   1   |   1   |    1    |    1    |     1     |

### **Programming the Full Adder**

```c
// Full Adder Logic Implementation

#include <stdio.h>
#include <debug.h>
#include <ch32v00x.h>

// Logic Gate Functions: AND, OR, XOR
int and_gate(int bit1, int bit2) {
    return bit1 & bit2;
}

int or_gate(int bit1, int bit2) {
    return bit1 | bit2;
}

int xor_gate(int bit1, int bit2) {
    return bit1 ^ bit2;
}

// GPIO Pin Configuration for Inputs and Outputs
void gpio_configure(void) {
    GPIO_InitTypeDef gpio_init_structure = {0}; 

    // Enable clocks for ports C and D
    RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOD, ENABLE);
    RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOC, ENABLE);
    
    // Configure input pins for A, B, Cin
    gpio_init_structure.GPIO_Pin = GPIO_Pin_1 | GPIO_Pin_2 | GPIO_Pin_3;
    gpio_init_structure.GPIO_Mode = GPIO_Mode_IPU;  // Input Pull-Up
    GPIO_Init(GPIOD, &gpio_init_structure);

    // Configure output pins for Sum and Carry
    gpio_init_structure.GPIO_Pin = GPIO_Pin_4 | GPIO_Pin_5;
    gpio_init_structure.GPIO_Mode = GPIO_Mode_Out_PP;  // Output Push-Pull
    gpio_init_structure.GPIO_Speed = GPIO_Speed_50MHz;  // Speed
    GPIO_Init(GPIOC, &gpio_init_structure);
}

// Main function for Full Adder execution
int main() {
    uint8_t A, B, Cin, Sum, Carry;
    uint8_t p, q, r, s, t; 

    // Initialize system clock and GPIOs
    NVIC_PriorityGroupConfig(NVIC_PriorityGroup_2);
    SystemCoreClockUpdate();
    Delay_Init();
    gpio_configure();

    // Continuous loop to read inputs and compute Full Adder output
    while(1) {
        A = GPIO_ReadInputDataBit(GPIOD, GPIO_Pin_1);
        B = GPIO_ReadInputDataBit(GPIOD, GPIO_Pin_2);
        Cin = GPIO_ReadInputDataBit(GPIOD, GPIO_Pin_3);

        // XOR, AND, OR operations to compute Sum and Carry
        s = xor_gate(A, B);
        Sum = xor_gate(Cin, s);
        p = and_gate(A, B);
        q = and_gate(B, Cin);
        r = and_gate(Cin, A);
        t = or_gate(p, q);
        Carry = or_gate(r, t);

        // Output the Sum to LED on GPIO Pin 4
        if (Sum == 0) {
            GPIO_WriteBit(GPIOC, GPIO_Pin_4, SET);
        } else {
            GPIO_WriteBit(GPIOC, GPIO_Pin_4, RESET);
        }

        // Output the Carry to LED on GPIO Pin 5
        if (Carry == 0) {
            GPIO_WriteBit(GPIOC, GPIO_Pin_5, SET);
        } else {
            GPIO_WriteBit(GPIOC, GPIO_Pin_5, RESET);
        }
    }
}
