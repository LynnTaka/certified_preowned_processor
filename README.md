# Project 1: certified_preowned_processor
### CS3650: Computer Architecture
Christian Badoy, Scott Lee, Lynn Takahashi

#### Objective:

This project adds to the ALU project in both functionality and complexity, and puts your understanding of Chapter 4.4 to the test. Gain more experience and understanding in Verilog.

(The name denotes the availability of helpful (if you make it so) resources from countless people who have "been there, done that". But the skills, knowledge, and experience would still be beautiful when they finally become yours.)


#### Tasks:

(100 pts) At a minimum, implement the single-cycle implementation as described in 4.4, handling the subset of instructions (ALU funcs, lw/sw, beq, jump) mentioned.

(20 pts) Implement 5-stage pipelining as shown in 4.7.



#### Code implementation  
An implementation of a 32-bit single cycle MIPS processor in Verilog: https://github.com/diadatp/mips_cpu
https://github.com/Hola39e/MIPS_Multi_Implementation#simulation-benchmarking-of-the-single-cycle-mips-processor

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

##### What we learned during implementation
- 

##### Why you do not want to use single cycle implementation
- inefficient, because the clock cycle must have the same length for every instruction

