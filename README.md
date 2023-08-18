# RISC-V_ISA

# Introduction to RISC-V ISA and GNU compiler toolchain
RISC-V is an open standard instruction set architecture (ISA) based on established reduced instruction set computer (RISC) principles. As a RISC architecture, the RISC-V ISA is a load–store architecture. Its floating-point instructions use IEEE 754 floating-point. Notable features of the RISC-V ISA include: instruction bit field locations chosen to simplify the use of multiplexers in a CPU,a design that is architecturally neutral, and a fixed location for the sign bit of immediate values to speed up sign extension.

The instruction set is designed for a wide range of uses. The base instruction set has a fixed length of 32-bit naturally aligned instructions, and the ISA supports variable length extensions where each instruction can be any number of 16-bit parcels in length. Subsets support small embedded systems, personal computers, supercomputers with vector processors, and warehouse-scale 19 inch rack-mounted parallel computers.

# Table of Contents

[Day 1](#day-1)

[Day 2](#day-2)

[Day 3](#day-3)

[Day 4](#day-4)

[Day 5](#day-5)

# Day_1 Introduction to RISC-V and GNU compiler toochain

<details>
 <summary> Introduction to RISC-V basic keywords
 </summary>

**Introduction to RISC-V basic keywords**

Why does a computer needs a RISC or CISC ISA?

Any computer program or software inorder to work on a computer hardware needs to communicate to the layout(chip present on system). Accomplishment of which requires a process to be followed. First the high level language program is converted to assembly level program(which follows a particular architecture RISC-V in this case). After which it's converted to machine level program for computer to understand.For communication between architeture to layout there is need for a interface, called HDL(Hardware Description Language).

Below image show the whole process of program or application execution.

![comb](https://github.com/DSatle/RISC-V_ISA/assets/140998466/501ac5d8-3d92-4ca2-af46-53b0c51e315d)

<details>
 <summary> Applications to Hardware
 </summary>

**Applications to Hardware**

Inorder to run any application on the computer system. Below process needs to be followed.

![Architure](https://github.com/DSatle/RISC-V_ISA/assets/140998466/4660910a-3379-476a-9983-20c82239c277)

Operating system, compiler, assembler all three combined are termed as system software.

The assembly language program is dependent on the processor and its architecture. Every architeture has its own assembly language program.
Converting assembly language program to machine level program is done using a specific process, which is elaborated in the flowchart below.

![Assembly to Physical implementation](https://github.com/DSatle/RISC-V_ISA/assets/140998466/a7955a90-e355-4abd-8fff-ce3472bdb43e)

<details>
 <summary> Applications to Hardware
 </summary>

 **Detailed description of detailed of Course content**

 








