
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

# Day 2 

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

# DAY 3 
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

# DAY 4
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

### Observations:-
* The synthesized and the expected design are different because the expected uses PMOS stacking which is not prefferable
* Using de-morgans law we can verify the design.
* The netlist file contains the hierarchy as mentioned in the design file.
* In the netlist file one NAND gate and two inverters are used instaed of using a and gate & or gate as specified in the design




## Various Flop Coding Styles and Optimization
### Why Flops and Flop Coding Styles	

**Why do we need a Flop?**

+ A flip-flop (often abbreviated as "flop") is a fundamental building block in digital circuit design.
+ It's a type of sequential logic element that stores binary information (0 or 1) and can change its output based on clock signals and input values.
+ In a combinational circuit, the output changes after the propagation delay of the circuit once inputs are changed.
+ During the propagation of data, if there are different paths with different propagation delays, then a glitch might occur.
+ There will be multiple glitches for multiple combinational circuits.
+ Hence, we need flops to store the data from the combinational circuits.
+ When a flop is used, the output of combinational circuit is stored in it and it is propagated only at the posedge or negedge of the clock so that the next combinational circuit gets a glitch free input thereby stabilising the output.
+ We use control pins like **set** and **reset** to initialise the flops.
+ They can be synchronous and asynchronous.

**D Flip-Flop with Asynchronous Reset**
+ When the reset is high, the output of the flip-flop is forced to 0, irrespective of the clock signal.
+ Else, on the positive edge of the clock, the stored value is updated at the output.

 `gvim dff_asyncres_syncres.v`
 
<img width="445" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/582609c7-faf6-4981-9643-ec5ad543b65f">

**D Flip_Flop with Asynchronous Set**
+ When the set is high, the output of the flip-flop is forced to 1, irrespective of the clock signal.
+ Else, on positive edge of the clock, the stored value is updated at the output.

`gvim dff_async_set.v`

<img width="357" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/f45ca71f-8eef-402a-a966-9035a51fa21d">

**D Flip-Flop with Synchronous Reset**
+ When the reset is high on the positive edge of the clock, the output of the flip-flop is forced to 0.
+ Else, on the positive edge of the clock, the stored value is updated at the output.

  `gvim dff_syncres.v`

<img width="409" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/d22a7aa2-059f-48bd-b0c4-32a294248c8b">

**D Flip-Flop with Asynchronous Reset and Synchronous Reset**
+ When the asynchronous resest is high, the output is forced to 0.
+ When the synchronous reset is high at the positive edge of the clock, the output is forced to 0.
+ Else, on the positive edge of the clock, the stored value is updated at the output.
+ Here, it is a combination of both synchronous and asynchronous reset DFF.

`gvim dff_asyncres_syncres.v`

<img width="439" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/8ee2f2a5-31e9-447c-a23f-b347fc7b642c">



### Lab Flop Synthesis Simulations 	

**D Flip-Flop with Asynchronous Reset**
+ **Simulation**
  - `cd VLSI/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
  - `iverilog dff_asyncres.v tb_dff_asyncres.v`
  - `./a.out`
  - `gtkwave tb_dff_asyncres.vcd`
  
![Screenshot from 2023-08-29 21-03-17](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/600b8311-de6c-4238-816b-f2ad7ce9b822)

<img width="500" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/326bf88d-74d9-407f-8c45-1e1e28ea1911">

+ **Synthesis**
  - `cd VLSI/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
  - `yosys`
  - `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
  - `read_verilog dff_asyncres.v`
  - `synth -top dff_asyncres`
  - `dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
  - `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
  - `show`

    <img width="925" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/92f225cf-a014-4a89-be7a-a9560a6d6359">

 **D Flip_Flop with Asynchronous Set**
 + **Simulation**
   - `cd VLSI/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `iverilog dff_async_set.v tb_dff_async_set.v`
   - `./a.out`
   - `gtkwave tb_dff_async_set.vcd`

![Screenshot from 2023-08-29 21-09-05](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/83f93fc8-f4e5-48b8-90b1-fcd696f9eb57)

<img width="500" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/51dd2cf5-ea6c-4b00-bf2a-5ae8674e2272">

+ **Synthesis**
  - `cd VLSI/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
  - `yosys`
  - `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
  - `read_verilog dff_async_set.v`
  - `synth -top dff_async_set`
  - `dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
  - `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
  - `show` 

<img width="922" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/87e93a5e-c904-4eca-b3a7-4657c8f8f0cc">

**D Flip-Flop with Synchronous Reset**
+ **Simulation**
   - `cd VLSI/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `iverilog dff_syncres.v tb_dff_syncres.v`
   - `./a.out`
   - `gtkwave tb_dff_syncres.vcd`

   ![Screenshot from 2023-08-29 21-11-28](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/fd90e31a-a9be-4b46-83e1-56f450201da4)

  <img width="500" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/472e9a2d-bb95-437d-b790-cfe72294ad07">
  

+ **Synthesis**
  - `cd VLSI/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
  - `yosys`
  - `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
  - `read_verilog dff_syncres.v`
  - `synth -top dff_syncres`
  - `dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib `
  - `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
  - `show`

<img width="925" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/ff5b11e7-11a8-40c9-9e08-e090eeb0f547">


### Interesting Optimisations

+ `gvim mult_2.v`

 <img width="434" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/d37ce39a-16c6-428a-a6be-ef6a5fc3c2aa">

+ `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `read_verilog mult_2.v`
+ `synth -top mul2`

 <img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/05011316-bfc4-41c3-8e87-46855d117243">

+ `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `show`

 <img width="305" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/fb4d176c-0d06-43e3-bad9-7945e02c2889">

+ `write_verilog -noattr mul2_netlist.v`
+ `!gvim mul2_netlist.v`
  
 <img width="436" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/9a0eca57-0656-4cb3-99f0-ad7a0d0f356e">

+ `gvim mult_8.v`

  <img width="443" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/3f9fa46f-56b9-43bf-8d46-325d75f76a95">

+ `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib  `
+ `read_verilog mult_8.v`
+ `synth -top mult8`

<img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/13359e0d-0676-4313-b791-3992655ee4f7">

+ `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `show`

<img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/4c8b811f-b793-45fa-a8e7-a65663ef3f74">

+ `write_verilog -noattr mult8_netlist.v`
+ `!gvim mult8_netlist.v`

<img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/37c89aea-497d-4e0d-99c5-c46dffd63b7d">

# Day 5
## Introduction to Optimisations 

### Combinational Optimisation 
	
+ Combinational logic refers to logic circuits where the outputs depend only on the current inputs and not on any previous states.
+ Combinational optimization is a field of study in computer science and operations research that focuses on finding the best possible solution from a finite set of options for problems that involve discrete variables and have no inherent notion of time.
+ Optimising the combinational logic circuit is squeezing the logic to get the most optimized digital design so that the circuit finally is area and power efficient.
+ Techniques for Optimisations:
  - **Constant propagation** is an optimization technique used in compiler design and digital circuit synthesis to improve the efficiency of code and circuit implementations by replacing variables or expressions with their constant values where applicable.
  - **Boolean logic optimization**, also known as logic minimization or Boolean function simplification, is a process in digital design that aims to simplify Boolean expressions or logic circuits by reducing the number of terms, literals, and gates required to implement a given logical function.



### Sequential Logic Optimisations 	

+ Sequential logic optimizations involve improving the efficiency, performance, and resource utilization of digital circuits that include memory elements like flip-flops and latches.
+ Optimizing sequential logic is crucial in ensuring that digital circuits meet timing requirements, consume minimal power, and occupy the least possible area while maintaining correct functionality.
+ Optimisation methods:
  - **Sequential constant propagation**, also known as constant propagation across sequential elements, is an optimization technique used in digital design to identify and propagate constant values through sequential logic elements like flip-flops and registers. This technique aims to replace variable values with their known constant values at various stages of the logic circuit, optimizing the design for better performance and resource utilization.
  - **State optimization**, also known as state minimization or state reduction, is an optimization technique used in digital design to reduce the number of states in finite state machines (FSMs) while preserving the original functionality.
  - **Sequential logic cloning**, also known as retiming-based cloning or register cloning, is a technique used in digital design to improve the performance of a circuit by duplicating or cloning existing registers (flip-flops) and introducing additional pipeline stages. This technique aims to balance the critical paths within a circuit and reduce its overall clock period, leading to improved timing performance and better overall efficiency.
  - **Retiming** is an optimization technique used in digital design to improve the performance of a circuit by repositioning registers (flip-flops) along its paths to balance the timing and reduce the critical path delay. The primary goal of retiming is to achieve a shorter clock period without changing the functionality of the circuit.
 


## Combinational Logic Optimisations


### opt_check 
	
+ `gvim opt_check.v`

  <img width="500" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/dad0961e-10d4-4a0c-9991-0ad6daea169f">

+ `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `read_verilog opt_check.v`
+ `synth -top opt_check`
+ `opt_clean -purge`
+ `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `show`

  <img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/44d6a65e-1405-49b6-a569-66a7c976308c">

  <img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/8861528b-55be-45e4-952e-c0600c811685">




### opt_check2 
	
+ `gvim opt_check2.v`

  <img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/d957a7b5-fb8a-4e59-a9d3-cb1730a7dd25">
  
+ `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `read_verilog opt_check2.v`
+ `synth -top opt_check2`
+ `opt_clean -purge`
+ `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `show`

<img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/c85299a9-10df-4b40-8f0f-f19ead681ad3">

<img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/d0b4fb18-71ff-4aa6-92b9-49eac8dd889b">


### opt_check3 
	
+ `gvim opt_check3.v`

<img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/3183db65-f77d-443a-9814-dc776c3c0990">

+ `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `read_verilog opt_check3.v`
+ `synth -top opt_check3`
+ `opt_clean -purge`
+ `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `show`

<img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/13709061-55c2-43ca-b798-c8398e1c7fdb">

<img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/2c885b4d-c274-4bae-abd0-15853f864f62">



### opt_check4 
	
+ `gvim opt_check4.v`

 <img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/75c65195-8f6b-416e-8074-306a46263746">

+ `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `read_verilog opt_check4.v`
+ `synth -top opt_check4`
+ `opt_clean -purge`
+ `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `show`

<img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/a1acd352-c271-4330-9fd8-6aafe72b8f11">

<img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/498cf442-ec8e-468e-a310-d1f93b93ce1a">


### multiple_module_opt 
	
+ `gvim multiple_module_opt.v`

 <img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/ad570bd8-44b5-4408-8715-02f1c5d15a29">

+ `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `read_verilog multiple_module_opt.v`
+ `synth -top multiple_module_opt`
+ `opt_clean -purge`
+ `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `show`
 
<img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/4c3fd4bc-c599-41cf-af42-c07280dcca11">

<img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/1344d22d-51f5-439e-bc34-96b2a742474e">



## Sequential Logic Optimisations


### dff_const1 

+ `gvim dff_const1.v`

<img width="331" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/abec2938-5f2c-4cd5-b369-103c1b09f098">

**Simulation**

+ `iverilog dff_const1.v tb_dff_const1.v`
+ `./a.out`
+ `gtkwave tb_dff_const1.vcd`
 
![Screenshot from 2023-08-29 21-27-43](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/3c21f77c-211f-4f8b-8839-ddad952d7d05)


<img width="503" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/51301173-fdbd-476c-842e-2d08078f020d">

**Synthesis**

+ `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `read_verilog dff_const1.v`
+ `synth -top dff_const1`
+ `dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib `
+ `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `show`

<img width="194" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/c542c8b4-3624-4a22-92c5-35a4b1458c35">

<img width="925" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/fa1d8b2f-431e-4836-8a75-8c2bd3ce326e">


### dff_const2 

+ `gvim dff_const2.v`

<img width="355" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/e0e6e4da-0429-49db-b687-d99ab365ed17">

**Simulation**

+  `iverilog dff_const2.v tb_dff_const2.v`
+ `/a.out`
+ `gtkwave tb_dff_const2.vcd`

![Screenshot from 2023-08-29 21-31-05](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/43190799-93e7-4685-895f-2940f18746da)

 <img width="500" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/a90d628f-dd7d-4ae6-8b4d-072b6a9960b9">

 **Synthesis**
 
+ `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `read_verilog dff_const2.v`
+ `synth -top dff_const2`
+ `dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib `
+ `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `show`

 <img width="206" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/d4859923-36a2-4cf2-bcef-6befaf718913">

<img width="305" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/8e3503dd-d315-426f-9a3e-bd487014600a">

### dff_const3 

+ `gvim dff_const3.v`

 <img width="272" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/3ce28559-0063-4ef1-9d7e-a3af839dd7e3">

**Simulation**

+ `iverilog dff_const3.v tb_dff_const3.v`
+ `./a.out`
+ `gtkwave tb_dff_const3.vcd`

![Screenshot from 2023-08-29 21-32-59](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/c5bd1ed5-037a-4412-ab10-1a818b8a3be5)

<img width="502" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/aed6c933-5c06-4687-ba9e-9c782626c030">

**Synthesis**

+ `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `read_verilog dff_const3.v`
+ `synth -top dff_const3`
+ `dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib `
+ `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `show`

<img width="197" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/7cc2308b-b988-4ba9-965f-06abf2472e2b">

<img width="922" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/bdea6f33-d357-47f4-a9fd-cc655dcce869">


### dff_const4 	

+ `gvim dff_const4.v`

<img width="311" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/bc5661c4-50c6-4ccf-8aab-a5ace3ccfa14">

**Simulation**

+ `iverilog dff_const4.v tb_dff_const4.v`
+ `./a.out`
+ `gtkwave tb_dff_const4.vcd`
 
![Screenshot from 2023-08-29 21-34-29](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/1737e73a-87d3-44a5-836a-a83299fd83c2)

<img width="500" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/1a9ee230-2ad6-4c92-8e37-0a753832180f">

**Synthesis**

+ `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `read_verilog dff_const4.v`
+ `synth -top dff_const4`
+ `dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib `
+ `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `show`

<img width="193" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/a152102c-a880-499d-98e6-f2d26201ea85">

<img width="306" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/4d4d33fc-11ec-4cb5-867d-2f34d892255a">


### dff_const5 	

+ `gvim dff_const5.v`

<img width="251" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/af7acfca-6fb0-4b62-bb1e-d32746d0c07e">

**Simulation**

+ `iverilog dff_const4.v tb_dff_const4.v`
+ `./a.out`
+ `gtkwave tb_dff_const4.vcd`
+ 
![Screenshot from 2023-08-29 21-36-34](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/2426474c-65db-4701-8696-3f19e07832ae)

<img width="500" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/7eb3b371-189e-483c-80d9-37d38c062cd2">

**Synthesis**

+ `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `read_verilog dff_const4.v`
+ `synth -top dff_const4`
+ `dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib `
+ `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `show`

 <img width="205" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/e2719af7-b746-4830-b04f-87df97143f86">

<img width="923" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/8d95c49d-9fd9-4d76-bba1-b893c6f163fc">



## Sequential Optimisations for Unused Outputs

### counter_opt 

 + `gvim counter_opt.v`

<img width="349" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/cb5798fa-2ee9-4cf0-9372-3da9ff17bd66">

+ `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `read_verilog counter_opt.v`
+ `synth -top counter_opt`
+ `dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `show`

<img width="184" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/1c876b33-9d26-4efe-95cf-5d0814415da5">

<img width="923" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/b65d5ac8-3961-4a7b-9e8a-18bc0229f104">


### counter_opt2 

+ `gvim counter_opt2.v`

 <img width="347" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/b6262d9a-5892-4360-91fa-18f7e2aa39e7">

+ `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `read_verilog counter_opt2.v`
+ `synth -top counter_opt2`
+ `dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `show`

 <img width="200" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/14aadea7-9607-40a8-b5ed-e48eb255cd10">

<img width="923" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/78af2250-6ee8-4d94-b91b-138cb2877b1e">


# Day 6
## GLS Synthesis-Simulation Mismatch and Blocking Non-blocking Statements

### GLS Concepts And Flow Using Iverilog 
 + **Gate Level Simualtion**
   - Gate-level simulation is a technique used in digital design and verification to validate the functionality of a digital circuit at the gate-level implementation.
   - It involves simulating the circuit using the actual logic gates and flip-flops that make up the design, as opposed to higher-level abstractions like RTL (Register Transfer Level) descriptions.
   - This type of simulation is typically performed after the logic synthesis process, where a high-level description of the design is transformed into a netlist of gates and flip-flops.
   - We perform this to verify logical correctness of the design after synthesizing it. Also ensuring the timing of the design is met.
  
<img width="608" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/6298b067-2f45-4dbc-ad25-762ac3d8be63">

+ **Synthesis-Simulation Mismatch**
  - A synthesis-simulation mismatch refers to a situation in digital design where the behavior of a circuit, as observed during simulation, doesn't match the expected or desired behavior of the circuit after it has been synthesized.
  - This discrepancy can occur due to various reasons, such as timing issues, optimization conflicts, and differences in modeling between the simulation and synthesis tools.
  - This mismatch is a critical concern in digital design because it indicates that the actual hardware implementation might not perform as expected, potentially leading to functional or timing failures in the fabricated chip.

+ **Blocking Statements**
  - Blocking statements are executed sequentially in the order they appear in the code and have an immediate effect on signal assignments.
  - Example:

  ``` v
   module BlockingExample(input A, input B, input C, output Y, output Z);
    wire temp;

    // Blocking assignment
    assign temp = A & B;

    always @(posedge C) begin
        // Blocking assignment
        Y = temp;
        Z = ~temp;
    end
   endmodule
  ```

+ **Non-Blocking Statements**
  - Non-blocking assignments are used to model concurrent signal updates, where all assignments are evaluated simultaneously and then scheduled to be updated at the end of the time step.
  - Example:
   ``` v
    module NonBlockingExample(input clock, input D, input reset, output reg Q);

    always @(posedge clock or posedge reset) begin
        if (reset)
            Q <= 0;  // Reset the flip-flop
        else
            Q <= D;  // Non-blocking assignment to update Q with D on clock edge
    end
  endmodule
   ```

+ **Caveats with Blocking Statements**
  + Blocking statements in hardware description languages like Verilog have their uses, but there are certain caveats and considerations to be aware of when working with them. Here are some important caveats associated with using blocking statements:
    - Procedural Execution: Blocking statements are executed sequentially in the order they appear within a procedural block (such as an always block). This can lead to unexpected behavior if the order of execution matters and is not well understood.
    - Lack of Parallelism: Blocking statements do not accurately represent the parallel nature of hardware. In hardware, multiple signals can update concurrently, but blocking statements model sequential behavior. As a result, using blocking statements for modeling complex concurrent logic can lead to incorrect simulations.
    - Race Conditions: When multiple blocking assignments operate on the same signal within the same procedural block, a race condition can occur. The outcome of such assignments depends on their order of execution, which might lead to inconsistent or unpredictable behavior.
    - Limited Representation of Hardware: Hardware systems are inherently concurrent and parallel, but blocking statements do not capture this aspect effectively. Using blocking assignments to model complex combinational or sequential logic can lead to models that are difficult to understand, maintain, and debug.
    - Combinatorial Loops: Incorrect use of blocking statements can lead to unintentional combinational logic loops, which can result in simulation or synthesis errors.
    - Debugging Challenges: Debugging code with many blocking assignments can be challenging, especially when trying to track down timing-related issues.
    - Not Suitable for Flip-Flops: Blocking assignments are not suitable for modeling flip-flop behavior. Non-blocking assignments (<=) are generally preferred for modeling flip-flop updates to ensure accurate representation of concurrent behavior.
    - Sequential Logic Misrepresentation: Using blocking assignments to model sequential logic might not capture the intended behavior accurately. Sequential elements like registers and flip-flops are better represented using non-blocking assignments.
    - Synthesis Implications: The behavior of blocking assignments might not translate well during synthesis, leading to potential mismatches between simulation and synthesis results.



## Labs on GLS and Synthesis-Simulation Mismatch

### ternary_operator_mux 

+ `gvim teranry_operator_mux.v`

<img width="370" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/8539ab94-8f5a-4bff-8465-eb8bb6ca83b8">

**Simulation**

+ `iverilog ternary_operator_mux.v tb_ternary_operator_mux.v`
+ `./a.out`
+ `gtkwave tb_ternary_operator_mux.vcd`

![1](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/f9242d1d-9d9c-4363-8b22-710ff588ccdc)

<img width="500" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/c675c505-880e-4c15-b079-3c528032c279">

**Synthesis**

+ `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `read_verilog ternary_operator_mux.v`
+ `synth -top ternary_operator_mux`
+ `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `show`

<img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/74fa07aa-5dc3-4f04-8fc1-babe67ded667">

<img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/9a4f4ebd-370f-45b5-a1c1-cd95b8e1e556">

**GLS to Gate-Level Simulation**

+ `iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v ternary_operator_mux_net.v tb_ternary_operator_mux.v`
+ `./a.out`
+ `gtkwave tb_bad_mux.vcd`

![2](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/bd1cc726-c4e7-41e7-9437-e9ac4a64fbea)

<img width="498" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/5c4652e6-8364-4e81-9cd3-f1795f5d321a">


### bad_mux 

 + `gvim bad_mux.v`

 <img width="290" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/deb388a2-8463-410b-b16e-5eaf81697d69">

**Simulation**

+ `iverilog bad_mux.v tb_bad_mux.v`
+ `./a.out`
+ `gtkwave tb_bad_mux.vcd`

![3](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/991df894-0139-4bf2-9d90-e7f42f9fdbc5)

<img width="500" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/46266c26-99ce-4a79-9e5c-9558ea15f407">

**Synthesis**

+ `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `read_verilog bad_mux.v`
+ `synth -top bad_mux`
+ `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `show`

<img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/a19eb270-87dd-40cc-95f8-3bd3cf02a396">

<img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/d15147f9-775d-44bb-93a5-d7249645d9bc">

**GLS to Gate-Level Simulation**

+ `iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v bad_mux_net.v tb_bad_mux.v`
+ `./a.out`
+ `gtkwave tb_bad_mux.vcd`

![4](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/28dd3771-a029-40d8-8290-2dca8b0e5cdc)
  
<img width="501" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/9d51d787-22d3-4495-95cc-c87c0ef71d17">


## Labs on Synth-Sim Mismatch for Blocking Statement


### blocking_caveat

+ `gvim blocking_caveat.v`

<img width="327" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/5827ea02-ec07-4164-9b9f-b064750ede9d">

**Simualtion**

+ `iverilog blocking_caveat.v tb_blocking_caveat.v`
+ `./a.out`
+ `gtkwave tb_blocking_caveat.vcd`

![5](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/363c84c2-0ab6-46a8-b93f-9c541c9ecf51)

<img width="501" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/c3b18d2e-d407-45c4-9e97-ec59042ec2bd">

**Synthesis**

+ `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `read_verilog blocking_caveat.v`
+ `synth -top blocking_caveat`
+ `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `show`

<img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/7f942ace-02b0-4421-8d20-5e7126cbb3df">

<img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/d660d89b-8a9a-43d3-9e78-ab1f7054a667">

**GLS to Gate-Level Simulation**

+ `iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v blocking_caveat_net.v tb_blocking_caveat.v`
+ `./a.out`
+ `gtkwave tb_blocking_caveat.vcd`

![6](https://github.com/Aatish-Om/pes_asic_class/assets/125562864/befb4c71-5ef6-401f-8f7a-b4506c042220)

<img width="503" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/c78704db-de4c-4958-880f-0747f78090d9">







