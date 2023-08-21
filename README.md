
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

### DAY 1

1. Introduction to RISCV ISA and GNU Compiler Toolchain
   - Introduction to Basic Keywords
   - Introduction: From Apps to Hardware
   - Detailed Course Content Description
   - Labwork for RISCV Toolchain

2. C Program
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
```

We compiled the program using the GCC compiler to get the output:

```bash
gcc sum1.c -o a.out
```
![atomdeb1](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/638c14fc-617e-45b4-969a-22eb76cd30cd)

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

### Application Binary Interface (ABI)

An Application Binary Interface (ABI) is a set of rules and conventions that govern how binary code interacts with other binary code. It enables interoperability between different software components written in different languages, compiled by different compilers, or running on different architectures.

### Memory Allocation for Double Words

64-bit numbers can be loaded into memory in little-endian or big-endian representation. Little-endian stores the least significant byte (LSB) at the lowest memory address, while big-endian stores the most significant byte (MSB) at the lowest memory address.

### Load, Add, and Store Instructions

Load instructions transfer data from memory to registers. Store instructions write data from registers into memory. Add instructions perform addition operations on registers.

### 32-Registers and their ABI Names

32 registers are present in the RISC-V RV64 architecture. ABI names for registers serve as standardized designations for their purpose and usage within a software ecosystem.

### Labwork using ABI Function Calls

We incorporated assembly language code into a C program using inline assembly or separate assembly files. We called assembly functions from C code, following the C calling convention. We reviewed examples of C and assembly files working together.

---


