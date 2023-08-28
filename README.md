
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
cus1to9.c
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
spike pk cus1to9.o
```
![lab2](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/cb22ac5d-fd42-4b00-926b-854f710724c4)

# RTL Design Using Verilog With sky130 Technology
## Softwares installation:
* **Iverilog** <br>
  
  **Commands to install iverilog:** <br>
  ```bash
  sudo apt install iverilog
  ``` 

  ![Screenshot from 2023-08-28 23-14-59](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/0d532319-3c54-4054-807d-5d655275f727)

* **GTKWave** <br>

  **Commands to install GTKWave:** <br> 
  ```bash
  sudo apt install gtkwave
  ``` 
  ![Screenshot from 2023-08-29 00-03-33](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/9f1cfcea-a47b-4c4f-8af4-5e418d79c2ba)

* **YOSYS** <br> 
  **Commands used to install YOSYS:** <br> 
  ```bash
  git clone https://github.com/YosysHQ/yosys.git
  ``` 
  ```bash
  cd yosys
  ```  
  ```bash
  sudo apt install make
  ``` 
  ```bash
  sudo apt-get update
  ```
  ```bash
  sudo apt-get install build-essential clang bison flex  libreadline-dev gawk tcl-dev libffi-dev git  graphviz xdot pkg-config python3 libboost-system-dev libboost-python-dev libboost-filesystem-dev zlib1g-dev
  ```
  ```bash
  make config-gcc
  ```
  ```bash
  make
  ```  

  ![Screenshot from 2023-08-28 23-18-34](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/89f461e0-f9c9-46dc-ab07-bb31c22d339a)

* **Commands used for vsdflow:**
  ```bash
  git clone https://github.com/kunalg123/vsdflow.git
  ```
  ```bash
  cd vsdflow
  ```
  ```bash
  chmod 777 opensource_eda_tool_install.sh
  ```
  ```bash
  ./opensource_eda_tool_install.sh
  ```
  
  ![Screenshot from 2023-08-28 23-48-58](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/3700644e-7fe5-4827-b882-b43e47d1e3d4)

# DAY 1 :
## Intro to Verilog RTL design and synthesis 
1) **Simulator** :- Tool(IVerilog) used to check/verify a design whenever the inputs change.
2) **Design** :- Set of verilog codes that have intended functionality.
3) **Testbench** :- Setup of applying stimulus to the design and verify the accuracy of the design.

**IVerilog based simulation flow :**

![263472723-3174e610-0ffa-4d71-86b4-f01f9b58677b](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/77c2512f-bb57-4ad2-9bfa-3fe5d68b7bff)

* Based on the changes in the inputs the output will be manipulated depending on the design.
* A vcd (Value Change Dump format) file will be generated.
* To view this vcd file we use gtkwave tool which displays the outut.
  
### Source codes and testbenches
**Commands used:**
```bash
git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop
```
![Screenshot from 2023-08-28 23-58-05](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/3548d698-9116-4289-ba20-e80b2a14b90e)

### Using iverilog to load mux.v program and tretbench from the source files and execute the VCD file
1) Get intp the folder containing the verilog code and the testbench files
```bash
iverilog good_mux.v tb_good_mux.v
```
2) This will generate the VCD file
```bash
./a.out
```
3) This will open up the waveform based on the testbench
```bash
gtkwave tb_good_mux.vcd
```
### Executing the a.out and .vcd files:

![Screenshot from 2023-08-29 00-21-37](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/e3bb52b3-ecae-420d-bb2c-754189f6552a)

### GTKWave output :

![Screenshot from 2023-08-29 00-23-18](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/e4941c03-ac00-4b86-b95c-7166cffe6f91)

### Analysing the logic and testbench
* **good_mux.v:**
![Screenshot from 2023-08-29 00-25-01](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/2013964d-42e7-4850-9470-4bad679f2272)

* **tb_good_mux.v:**
![Screenshot from 2023-08-29 00-27-09](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/b9c19a76-456c-43ab-91f1-e00ac39350bb)

### YOSYS and Logic Synthesis

![263510914-5edd408a-fb91-4252-9ebe-307d19856b6b](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/bd65051e-6bdc-4252-914d-1003087d2c7c)

* The design file and the .lib files are applied to YOSYS to get a synthesised output(netlist)
* **read_verilog:** used to read the design
* **read_liberty:** used to read the library files
* **write_verilog:** used on netlist file to get netlist


### Veifying the synthesis:
![263511084-db9309df-4c2f-41f9-a314-3973345cd399](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/4d8d8195-0c24-4739-a559-95b306766770)

* the same **.tb** file can be used here along with the netlist file generated
* **RTL design:** Behavioural representation of the required design (in VHDL)
* **Synthesis:** Converting RTL into gate level/netlist
* **Synthesiszer:** (YOSYS) converts RTL into netlist

### .lib files:
* It consists of all the standard library files(collection of logical modules and all gates of different delays)
* Why gates of different delays:-
  	i) To satisfy the timing delays of different combinational logics
	ii) T_clk > T_cq_A + T_comb + T_setup_b (we need fast gates here)
	iii) T_hold < Tcq_A + T_comb (need slow gates)

## Lab on YOSYS

We read the **.lib** and design diles on yosys to get the netlist output 
**Commands used:**
```bash
read_liberty -lib /path to .lib file
```
```bash
read_verilog good_mux.v
```
```bash
synth -top module_name
```
```bash
abc -liberty /path to .lib file/
```
```bash
show
```
```bash
write_verilog -noattr good_mux_netlist.v
```
```bash
!gvim good_mux_netlist.v
```

* **read_liberty -lib /path to .lib file/** // It reads all the components in the .lib file
* **read_verilog good_mux.v** // This will read the desgn verilog file
![Screenshot from 2023-08-29 00-47-40](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/675afcf2-129e-4c24-854d-5429da268a19)

* **synth -top module_name** // This will synthesis the module specified
![Screenshot from 2023-08-29 00-48-53](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/8aa8abf0-952a-46d5-8a46-856149fb535d)

* **abc -liberty /path to .lib file/** // This will generate the netlist file based on the .lib file mentioned

![Screenshot from 2023-08-29 00-50-31](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/b4da6b61-b419-4c1e-b504-afef43751453)

* **show** // Used to see the synthesised output / netlist
  
![Screenshot from 2023-08-29 00-51-11](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/11419762-017f-47b9-a9d8-68b0d05d88ea)

* **write_verilog -noattr good_mux_netlist.v** // This command writes the netlist into the specifies file
* **!gvim good_mux_netlist.v** // This command will display the netlist.v file

![Screenshot from 2023-08-29 00-56-40](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/667878d2-f4bd-4853-a765-8f60aaf075a2)

# DAY-2
## .lib files
### commands used in terminal :
```bash
gvim /path to the .lib file/
```
### commands used in vim:
```bash
syn off // Switches off the highlighting of the syntax
```
```bash
se un  // used to enable the line numbers
```
```bash
/cell  // used to find a word cell
```
```bash
vsp   // Opens another window of the same file
```
it contains:-

* Conditions of PVT(Pressure Voltage Temperature) for proper working
* Default values/units
* time_unit : "1ns";
** voltage_unit : "1V";
** leakage_power_unit : "1nW";
** current_unit : "1mA";
** pulling_resistance_unit : "1kohm";
** capacitive_load_unit(1.0000000000, "pf");
** default_operating_conditions : "tt_025C_1v80";
* Standard cells
* Leakage powers of all the cells for different inputs
* About the technology("CMOS")
 
### .lib file:

![263531024-d1c0aadb-6cef-4fab-a7a9-738635e677ea](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/9117eb91-2469-4966-91d6-d47ae21f2404)

### Different versions of the and2 gate:-
### **and2_0 :**

![263534366-f51956e2-5536-49c5-bead-3d4a07af4b8f](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/06549be4-bf4a-4cde-b704-ba52ba8aa20d)

### **and2_2:**
![263534384-03ab1e2b-1467-45dc-8abb-bf9a07600df5](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/8c127731-68c9-4b7b-8df6-1412bb9963d5)

### **and2_4:**
![263534542-e4d5275d-7e0a-4591-a89c-a35658d59a48](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/63db148c-f226-41b8-b65f-c32203b184f3)

### Observation:-
* In terms of area and power :- **and2_4** > **and2_2** > **and2_0**
* **Wider cells** occupy **high area** and consume **high power** and the **delay is low**
* **smaller cells** occupy **low area** and consume **low power** and the **delay is high**

## Synthesizing a module named multiple_modules.v using YOSYS
* It contains two sub-modules
![263765016-ffa7add0-f537-4075-b6be-a2ad4564c822](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/c348bf9f-6989-4d47-bc65-794b5bb51192)

### **Commands used:**
```bash
read_liberty -lib /path to .lib file/    // reads the .lib file onto YOSYS
```
```bash
read_verilog multiple_modules.v          // reads the .v file specified
```
```bash
synth -top multiple-modules              // synthesizes the design by taking specified module as top module  
```
```bash
abc -liberty /path to .lib file/         // links the .lib file to the design
```
```bash
show                                     // displays the synthesized design
```
```bash
write_verilog -noattr multiple_modules_hier.v    // writes the netlist into the specified file 
```
```bash
!gvim multiple_modules_hier.v            // displays the netlist file
```

### Opening YOSYS and reading the .lib file:

![Screenshot from 2023-08-29 00-47-40](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/a321d570-e79f-493a-8f89-9cd680df9093)

### Reading the multiple_modules.v file on YOSYS:

![263765567-ffd41d13-4c03-4617-9c32-c7c225df6459](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/9c12ba30-2ba3-431b-bdb6-436ea8ad6a94)

### Using synth command to synthesize the design:

![263765682-8e1161bb-86d6-4137-a782-7f6552f95ad5](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/e09efc08-b0be-478f-a259-2a95f1987634)

![263765700-7e3dcc6f-bfc2-486d-a397-4f69d9bd790d](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/ee94e8d4-5041-4993-8999-d73194e42e81)

  

### Linking the .lib file to the design:

![263766278-59c0eea0-b330-474f-bb04-8c547b118898](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/d94de9e5-e4fc-4494-82e5-9cf996f301a7)


### Synthesized output:

![263765949-09d1dc75-9565-435d-ac31-741890270149](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/db1602aa-5306-4c2d-a959-553ee8463039)

### Using write_verilog to write the netlist:-

![263766570-6ff263a1-cc1b-4174-a357-60581bf9b17a](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/d7ef05d7-dd70-4dd0-8107-69a286ccfc9b)

### The output netlist:
![263767826-c0ba177d-7a18-4763-9d41-6b158e7e515c](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/ef4a7cf4-186a-4fb7-a0fc-27b73df27283)

### Expected v/s synthesized design:

### Observations:-
* The synthesized and the expected design are different because the expected uses PMOS stacking which is not prefferable
* Using de-morgans law we can verify the design.
* The netlist file contains the hierarchy as mentioned in the design file.
* In the netlist file one NAND gate and two inverters are used instaed of using a and gate & or gate as specified in the design







