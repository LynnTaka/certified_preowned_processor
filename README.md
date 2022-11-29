# Project 1: certified_preowned_processor
### CS3650: Computer Architecture
Christian Badoy, Scott Lee, Lynn Takahashi

#### Objective:

This project adds to the ALU project in both functionality and complexity, and puts your understanding of Chapter 4.4 to the test. Gain more experience and understanding in Verilog.

(The name denotes the availability of helpful (if you make it so) resources from countless people who have "been there, done that". But the skills, knowledge, and experience would still be beautiful when they finally become yours.)


#### Tasks:

(100 pts) At a minimum, implement the single-cycle implementation as described in 4.4, handling the subset of instructions (ALU funcs, lw/sw, beq, jump) mentioned.

(20 pts) Implement 5-stage pipelining as shown in 4.7.



#### Code implementation and Information References
An implementation of a single cycle MIPS processor in Verilog: https://github.com/diadatp/mips_cpu

An implementation of a single cycle and multi cycle MIPS processor:
https://github.com/Hola39e/MIPS_Multi_Implementation#simulation-benchmarking-of-the-single-cycle-mips-processor

Information: https://electrobinary.blogspot.com/2021/02/mips-processor-design-using-verilog-part1.html

#### How to run
##### single-cycle MIPS processor
$ cd Single_Cycle<br>
$ iverilog -o MIPS_wave -y ./ tb_MIPS_Single_Cycle.v<br>
$ vvp -n MIPS_wave --lxt2<br>
$ gtkwave MIPS_wave.vcd<br>

##### 5 stage pipeline MIPS processor
$ cd MIPS_Pipeline<br>
$ iverilog -o MIPS_wave -y ./ tb_MIPS_Pipeline.v<br>
$ vvp -n MIPS_wave --lxt2<br>
$ gtkwave MIPS_wave.vcd<br>

- Our waveforms are saved as MIPS_wave_simulation.gtkw

#### What we learned:
##### General
- The simplest possible implementation covers lw, sw, beq, the ALU instructions, and jump.
- The opcode determines the settings for the ALUOp bits
- For this implementation each memory is a 64 word x 32 bit array
- there are seven control signals: RegDst, RegWrite, ALUSrc, PCSrc, MemRead, MemWrite, MemtoReg

##### There are three instruction classes
- For R-type instructions: | 0  31:26 | rs 25:21 | rt 20:16 | rd 15:11 | shamt 10:6 | funct 5:0 |
- load or store instructions: | 35 or 43 31:26 | rs 25:21 | rt 20:16 | address 15:0 |
- branch instructions: | 4 31:26 | rs 25:21 | rt 20:16 | address 15:0 |
- opcode contained in bits 31:26
- two registers to be read are in the rs (25:21) and rt (20:16) fields.
- base register for lw and sw in rs
- for loads, rt is the destination register, for stores rt, is the source register

##### Why you do not want to use single cycle implementation
- inefficient, because the clock cycle must have the same length for every instruction
- clock cycle is determined only by worst-case delay for every instruction
- violates the idea of making the common case fast

##### Pipelined datapath and control
- five stages
- IF: instruction fetch
- ID: instruction decode and register file read
- EX: execution or address calculation
- MEM: data memory access
- WB: writeback
- improves throughput and program execution time
- clock cycle time is limited by longest pipeline stage

##### Components of the processor datapath:
1. Instruction Memory:
- store instructions of the program
- supply instruction locatted at given address
- load instruction memory using ReadMem

2. Program Counter
- holds address of the current instruction
- increment address by 4
- new instruction executed at every clock cycle

3. Register File:
- this module will enclose all the independent registers of the processor, to perform write and read operations
- we can load register memory using MemRead from a memory file

4. ALU:
 - ALU will be required to perofrm operations on the data provided to it

5. Sign Extension Unit

6. Data Memory:
- load data memory using ReadMem function
- for lw and sw instructions compute the memory address from which we have to fetch or store data.

7. Shifter (for BEQ)
- if condition is false, execute next instruction
- if condition is true, branch to next instruction address
