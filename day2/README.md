## DAY 2 
**Introduction to ABI and Basic Verification Flow**
+ Application Binary Interface
  - Introduction to ABI
  - Memory Allocation for Double Words
  - Load, Add and Store Instructions
  - 32-Registers and their ABI Names](#32-registers-and-their-abi-names

+ Labwork using ABI Function Calls
  - Algorithm for C Program using ASM
  - Review ASM Function Calls
  - Simulate C Program using Function Call
    
# Application Binary Interface
## Introduction to ABI
+ An Application Binary Interface (ABI) is a set of rules and conventions that dictate how binary code interacts with and communicates with other binary code, typically at the level of machine code or compiled code. In simpler terms, it defines the interface between two software components or systems that are written in different programming languages, compiled by different compilers, or running on different hardware architectures.
+ The ABI is crucial for enabling interoperability between different software components, such as different libraries, object files, or even entire programs. It allows components compiled independently and potentially on different platforms to work seamlessly together by adhering to a common set of rules for communication and data representation.
## Memmory Allocation for Double Words
64-bit number (or any multi-byte value) can be loaded into memory in little-endian or big-endian. It involves understanding the byte order and arranging the bytes accordingly
1. **Little-Endian:**
In little-endian representation, you store the least significant byte (LSB) at the lowest memory address and the most significant byte (MSB) at the highest memory address.
2. **Big-Endian:**
In big-endian representation, you store the most significant byte (MSB) at the lowest memory address and the least significant byte (LSB) at the highest memory address.
## Load, Add and Store Instructions
Load, Add, and Store instructions are fundamental operations in computer architecture and assembly programming. They are often used to manipulate data within a computer's memory and registers.
1. **Load Instructions:**
Load instructions are used to transfer data from memory to registers. They allow you to fetch data from a specified memory address and place it into a register for further processing.
Example `ld x11, 8(x7)`

In this Example
- `ld` is the load double-word instruction.
- `x11` is the destination register.
- `8(x7)` is the memory address pointed to by register `x5` (base address + offset).
2. **Store Instructions:**
Store instructions are used to write data from registers into memory.They store values from registers into memory addresses

Example `sd x7, 8(x9)`

In this Example
- `sd` is the store double-word instruction.
- `x7` is the source register.
- `8(x9)` is the memory address pointed to by register `x9` (base address + offset).
3. Add Instructions:
  Add instructions are used to perform addition operations on registers. They add the values of two source registers and store the result in a destination register.

Example `add x9, x10, x11`

In this Example
- `add` is the add instruction.
- `x1` is the destination register.
- `x12` and `x13` are the source registers.
## 32-Registers and their ABI Names
The choice of the number of registers in a processor's architecture, such as the RISC-V RV64 architecture with its 32 general-purpose registers, involves a trade-off between various factors. While modern processors can have more registers but increasing the number of registers could lead to larger instructions, which would take up more memory and potentially slow down instruction fetch and decode.
#### ABI Names
ABI names for registers serve as a standardized way to designate the purpose and usage of specific registers within a software ecosystem. These names play a critical role in maintaining compatibility, optimizing code generation, and facilitating communication between different software components. 
#Lab
  code:
  ```c
  #include <stdio.h>
  
  extern int load(int x, int y);
  
  int main()
  {
    int result = 0;
    int count = 9;
    result = load(0x0, count+1);
    printf("Sum of numbers from 1 to 9 is %d\n", result);
  }
  ```
```
**Asseembly File**
`load.s`
``` s
.section .text
.global load
.type load, @function

load:

add a5, a0, zero
add a2, a0, a1
add a3, a0, zero

loop:

add a5, a3, a5
addi a3, a3, 1
blt a3, a2, loop
add a0, a5, zero
ret
```
Run the following files using command
```
riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o custom1to9.o custom1to9.c load.s
```
this will generate `custom1to9.o`
Run this command for the output `custom1to9.o`
![image](https://github.com/KKiranR/pes_asic_class/assets/89727621/174cefee-f11c-4f22-8340-4ad92b8b962b)

