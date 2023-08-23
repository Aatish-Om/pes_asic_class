
---

# VLSI Physical Design for ASICs

## Objective

The objective of VLSI (Very Large Scale Integration) physical design for ASICs (Application-Specific Integrated Circuits) is to transform a logical design description (RTL - Register Transfer Level) into a physical layout that can be fabricated as an integrated circuit. This involves translating the high-level functional representation of the circuit into a physical implementation that meets design constraints, performance targets, and manufacturability requirements.

## Skill Outcomes

- Architectural Design
- RTL Design / Behavioral Modeling
- Floorplanning
- Placement
- Clock Tree Synthesis
- Routing

## Installation

You can find the necessary materials and scripts for this course on this [GitHub repository](https://github.com/kunalg123/riscv_workshop_collaterals/blob/master/run.sh). To get started:

1. Download the `run.sh` script.
2. Open your terminal.
3. Navigate to your "Downloads" directory using the `cd Downloads` command.
4. Run the script using `./run.sh`.

## Table of Contents

# DAY 1

**1. Introduction to RISCV ISA and GNU Compiler Toolchain**
   - Introduction to Basic Keywords
   - Introduction: From Apps to Hardware
   - Detailed Course Content Description
   - Labwork for RISCV Toolchain

**2. C Program**
   - RISCV GCC Compiler and Disassemble
   - Spike Simulation and Debug
   - Integer Number Representation
   - 64-bit Unsigned Numbers
   - 64-bit Signed Numbers
   - Labwork for Signed and Unsigned Numbers

### Introduction to Basic Keywords

#### ISA (Instruction Set Architecture)

ISA defines the interface between a computer's hardware and its software, specifying how the processor and its components interact with software instructions for task execution. It includes instructions, addressing modes, data types, registers, memory organization, and execution mechanisms.

#### RISC-V (Reduced Instruction Set Computing - Five)

RISC-V is an open-source ISA that simplifies the instruction set with a focus on a smaller set of instructions, each executable in a single clock cycle. This approach often leads to faster execution of instructions.

### From Apps to Hardware

- **Apps**: Application software performs specific tasks for end-users.
- **System Software**: Acts as an intermediary between hardware and user-facing application software. Manages resources, enables execution of applications, and ensures system functionality, security, and performance.
- **Operating System**: Manages hardware resources and provides services for users and applications, such as memory management, process scheduling, and user interfaces.
- **Compiler**: Translates high-level programming code into assembly-level language.
- **Assembler**: Translates assembly language code into machine code for execution.
- **RTL (Register Transfer Level)**: Represents digital circuit behavior in terms of registers and data transfer operations.
- **Hardware**: Physical components of a computer system or electronic device.

### Detail Description of Course Content

- **Pseudo Instructions**: Simplify programming, improve code readability, and reduce explicit instructions. Examples include `li` and `mv`.
- **Base Integer Instructions**: Fundamental instructions for arithmetic, logical, and data movement operations. Examples include `add`, `sub`, `and`, `or`, `xor`, `sll`.
- **Multiply Extension Instructions**: Enhance the instruction set for efficient multiplication and multiply-accumulate operations. Examples include `mul`, `mulh`, `mulhu`, `mulhsu`.
- **Single and Double Precision Floating Point Extension**: Support for single-precision (32-bit) and double-precision (64-bit) floating-point arithmetic operations.
- **Application Binary Interface (ABI)**: Rules and conventions for software component interaction at the binary level, including function calls, parameter passing, memory allocation, etc.
- **Memory Allocation and Stack Pointer**: Managing memory segments for program data and tracking execution position on the call stack.

---



Sure, here's the provided information rephrased and converted into a Markdown (.md) format:

---

## Labwork for RISCV Toolchain

### C Program

We created a C program using the text editor Leafpad to calculate the sum from 1 to n:

```c
leafpad sum1.c
```
```c
#include<stdio.h>

int main(){
    int i, sum=0, n=111;
    for (i=1; i<=n; ++i) {
        sum += i;
    }
    printf("Sum of numbers from 1 to %d is %d \n", n, sum);
    return 0;
}



We compiled the program using the GCC compiler to get the output:

```bash
gcc sum1.c -o a.out
```
``![q1](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/00da03d0-d55e-40be-89ba-0e404a969645)


### RISCV GCC Compiler and Disassemble

We compiled the C program using the RISC-V GCC compiler:

```bash
riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum1.o sum1.c
```
![atom1](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/178dceda-4de3-48eb-b66e-4ab895d9d83d)

We checked the creation of the object file using the command:

```bash
ls -ltr sum1.c
```

To disassemble the ALP code for the C program, we used:

```bash
riscv64-unknown-elf-objdump -d sum1.o | less
```

To view the main section, we used the `/main` command. With the `-O1` optimization, the number of instructions was 15.<img width="453" alt="261329510-98843b92-0beb-4bfc-ba4b-1dac5c93ed3c" src="https://github.com/Aatish-Om/pes_asic_class/assets/125562864/a8bf4bd1-3e4c-42f0-ae0f-9addfdd86b95">

### Spike Simulation and Debug

We used `spike pk sum1.o` to check if the instructions produced the correct output. For debugging, we used `spike -d pk sum1.c`. The contents of the registers could also be viewed.

### Integer Number Representation

**Unsigned Numbers**: Represent magnitudes without direction or sign. Range: [0, (2^n)-1]![atom2]


**Signed Numbers**: Represent positive, negative, and zero values. Range: Positive: [0, 2^(n-1)-1] Negative: [-1 to 2^(n-1)]![atom3]


We created C programs to show the maximum and minimum values of 64-bit unsigned and signed numbers.
```c
#include <stdio.h>
#include <math.h>

int main(){
	unsigned long long int max = (unsigned long long int) (pow(2,64) -1);
	unsigned long long int min = (unsigned long long int) (pow(2,64) *(-1));
	printf("lowest number represented by unsigned 64-bit integer is %llu\n",min);
	printf("highest number represented by unsigned 64-bit integer is %llu\n",max);
	return 0;
}
```
![atom2](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/03fe5e29-0aea-4ba9-9576-09d546a593f6)

```c
#include <stdio.h>
#include <math.h>

int main(){
	long long int max = (long long int) (pow(2,63) -1);
	long long int min = (long long int) (pow(2,63) *(-1));
	printf("lowest number represented by signed 64-bit integer is %lld\n",min);
	printf("highest number represented by signed 64-bit integer is %lld\n",max);
	return 0;
}
```
![atom3](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/72e8803f-6e31-4512-8f7a-93541a4172c6)

# Day 2:

## Application Binary Interface
Introduction to ABI
An Application Binary Interface (ABI) is a set of rules and conventions that dictate how binary code interacts with and communicates with other binary code, typically at the level of machine code or compiled code. In simpler terms, it defines the interface between two software components or systems that are written in different programming languages, compiled by different compilers, or running on different hardware architectures.

### Memory Allocation for Double Words
64-bit number (or any multi-byte value) can be loaded into memory in little-endian or big-endian. It involves understanding the byte order and arranging the bytes accordingly:

* Little-Endian: In little-endian representation, you store the least significant byte (LSB) at the lowest memory address and the most significant byte (MSB) at the highest memory address.
* Big-Endian: In big-endian representation, you store the most significant byte (MSB) at the lowest memory address and the least significant byte (LSB) at the highest memory address.
  
### Load, Add and Store Instructions
Load, Add, and Store instructions are fundamental operations in computer architecture and assembly programming. They are often used to manipulate data within a computer's memory and registers.
Load, Add and Store Instructions
Load, Add, and Store instructions are fundamental operations in computer architecture and assembly programming. They are often used to manipulate data within a computer's memory and registers.

1. **Load Instructions:** Load instructions are used to transfer data from memory to registers. They allow you to fetch data from a specified memory address and place it into a register for further processing.
Example ```ld x6, 8(x5) ```

In this Example

* ```ld``` is the load double-word instruction.
* ```x6``` is the destination register.
* ```8(x5)``` is the memory address pointed to by register x5 (base address + offset).
2. **Store Instructions:** Store instructions are used to write data from registers into memory.They store values from registers into memory addresses
Example ```sd x8, 8(x9)```

In this Example

* ```sd``` is the store double-word instruction.
* ```x8``` is the source register.
* ```8(x9)``` is the memory address pointed to by register x9 (base address + offset).

3.**Add Instructions:** Add instructions are used to perform addition operations on registers. They add the values of two source registers and store the result in a destination register.
Example ```add x9, x10, x11```

In this Example

* ```add``` is the add instruction.
* ```x9``` is the destination register.
* ```x10``` and ```x11``` are the source registers.

### 32-Registers and their ABI Names
The choice of the number of registers in a processor's architecture, such as the RISC-V RV64 architecture with its 32 general-purpose registers, involves a trade-off between various factors. While modern processors can have more registers but increasing the number of registers could lead to larger instructions, which would take up more memory and potentially slow down instruction fetch and decode.

### ABI Names
ABI names for registers serve as a standardized way to designate the purpose and usage of specific registers within a software ecosystem. These names play a critical role in maintaining compatibility, optimizing code generation, and facilitating communication between different software components.


<img width="267" alt="regfile" src="https://github.com/Aatish-Om/pes_asic_class/assets/125562864/590d6618-7db6-4c32-83b0-386d4772f5cc">


## Labwork using ABI Function Calls

### Algorithm for C Program using ASM
* Incorporating assembly language code into a C program can be done using inline assembly or by linking separate assembly files with your C code.
* When you call an assembly function from your C code, the C calling convention is followed, including pushing arguments onto the stack or passing them in registers as required.
* The program executes the assembly function, following the assembly instructions you've provided.

### Review ASM Function Calls
* We wrote C code in one file and your assembly code in a separate file.
* In the assembly file, we declared assembly functions with appropriate signatures that match the calling conventions of your platform.

C program:
```c
custom1to9.c
```

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

Assembly File:
```bash
load.s
```

```bash
.section .text
.global load
.type load, @function

load:

add a4, a0, zero
add a2, a0, a1
add a3, a0, zero

loop:

add a4, a3, a4
addi a3, a3, 1
blt a3, a2, loop
add a0, a4, zero
ret
```
## Simulate C Program using Function Call
**Compilation**: To compile C code and Asseembly file use the command

```bash
riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o cus1to9.o cus1to9.c load.s
```
**Execution**: To execute the object file run the command
```bash
spike pk custom1to9.o
```
![lab2](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/cb22ac5d-fd42-4b00-926b-854f710724c4)









