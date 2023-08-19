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

 
**Applications to Hardware**

Inorder to run any application on the computer system. Below process needs to be followed.

![Architure](https://github.com/DSatle/RISC-V_ISA/assets/140998466/4660910a-3379-476a-9983-20c82239c277)

Operating system, compiler, assembler all three combined are termed as system software.

The assembly language program is dependent on the processor and its architecture. Every architeture has its own assembly language program.
Converting assembly language program to machine level program is done using a specific process, which is elaborated in the flowchart below.

![Assembly to Physical implementation](https://github.com/DSatle/RISC-V_ISA/assets/140998466/a7955a90-e355-4abd-8fff-ce3472bdb43e)


 **Detailed description of detailed of Course content**
 
The course deals with a elaborative study of the instruction types present in the RISC-V architeture. Here I have mentioned types of instruction sets present in the RISC-V architecture

1. Pseduo Instuctions- Examples of pseduo instructions are **mv,li,ret**.

2. Base Integer Instructions - The nomenclature for these instructions is **RV64I** here RV stands for RISC-V, 64 stands for 64 bit integer. Few examples of base integer instructions are **lui,addi,jalr,auipc,ld**.

3. Multiply extension- If there is multiply or divide operation needs to be performed on the numbers these instructions are used. Nomencalture for these instructions is RV64M, and if its multiplication or division on base integer than its nomencleture would be RV64Im

4. Single & double precision floating point extension- If add/sub/divide/multiply is performed on the floating point number this instruction set is used. RV64F & RV64D. Few examples are **flw,fadd.s,fcvt.s.s,fmv.x.d,fsd,fmul.s,fdiv.s,fmv.x.d**. A CPU which performs all above operations is termed as RV64IMFD.

5. Application Binary interface- This is made so that application programmers can access resources of processor like register. Few examples are **a0,SP,s0.**

6. Memory allocation & stack pointer- Transfer of data from memory to registers, stack pointer. Example **ra,24(sp),s0, 16(sp),Sp,32**.

<details>
 <summary> Labwork for RISC-V software toolchain
 </summary>

**Labwork for RISC-V software toolchain**

C Program to compute sum from 1 to N.

Here I wrote a C program to calculate the sum of n numbers. Input is taken from user. C code for is as follows

 ```
#include <stdio.h>
int main()
{
    int n,sum=0;
    printf("Enter n: ");
    scanf("%d",&n);
    for(int i=1;i<=n;i++)
    sum =sum+i;
printf("sum of %d numbers is %d\n",n,sum);
return 1;
}
  ```
To get the output of the above program i wrote following commands 

```
  gcc file_name.c
  ./a.out
```
The following I got in when program is run on the system. The image shows the sum first 100 natural numbers 

![7](https://github.com/DSatle/RISC-V_ISA/assets/140998466/a13a608c-fdec-4e76-9011-08a5d0180b80)


**RISC-V GCC compile And Dissemble**
Here I observed the difference in RISC-V instructions first I used the command 
```
/home/divyam/riscv_toolchain/riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-ubuntu14/bin/risv64-unknown-elf-gcc-O1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
```
The following assembly level codes list was way too long to filtered the main portion in which we are interested is seen by the following command

```
riscv64-unknown-elf-objdump -d sum1ton.o | less
```
The following instructions were obtained 

![-01 fast less](https://github.com/DSatle/RISC-V_ISA/assets/140998466/cc15dd2f-e3d4-456a-83e6-cda253b051ee)


After this I entered the command 

```
/home/divyam/riscv_toolchain/riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-ubuntu14/bin/risv64-unknown-elf-gcc -Ofast -ch=rv64i -o sum1ton.o sum1ton.c

```
Using the less command above mentioned I got the following results

![ofast less](https://github.com/DSatle/RISC-V_ISA/assets/140998466/47a88ccf-8553-410e-b229-9e67a13d3c22)


**Spike simulation and debug**

To get the same output on RISCV I used the following commands 
```
/home/divyam/riscv_toolchain/riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-ubuntu14/bin/spike pk sum1ton.o
```

![1](https://github.com/DSatle/RISC-V_ISA/assets/140998466/32bd10ec-3a6b-4de3-9752-c858435462c0)

Now here are the commands which I used to debug the assembly level program 
```
/home/divyam/riscv_toolchain/riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-ubuntu14/bin/spike -d pk sum1ton.o
```
Following are the the debug commands I used 
```
until pc 0 1000b0 // This indicates start and end address for the commands.

reg 0 a2 // This command is used to check the contents of the register

lui // load upper immediate

q // quit

reg 0 sp // Knowing value stored in Stack Pointer

addi // add immediate 
```
Below is the screenshot for the commands used

![2](https://github.com/DSatle/RISC-V_ISA/assets/140998466/98e7321a-d0d1-4d7d-8d5a-fc75105502ee)

Below is a self explanatory image of 64 bit instruction and instruction used in the RISC-V

![3](https://github.com/DSatle/RISC-V_ISA/assets/140998466/2cd96086-bb08-42f2-beb5-d15e2002fa8c)


<details>
 <summary> Integer number representation
 </summary>
 
**Integer number representation**

**64-bit Number System For Unsigned numbers**
Here first of all we will get familiar with few basic terminologies

Double Word:- Entire 64 bit number in processor language is called double word.

Word:- 32 bit number in processor language 

Byte:- Group of 8 bits.

Total no. of pattern that can be formed is = (2^n -1); where n:- number of bits.

RISC-V doubleword can represent "0" to (2^64-1) unsigned numbers. 

The following images shows terminologies range and binary to decimal conversion

![Capture](https://github.com/DSatle/RISC-V_ISA/assets/140998466/8d9c0947-2640-452a-a6c8-23d738686f78)

![range](https://github.com/DSatle/RISC-V_ISA/assets/140998466/3961e697-5815-46c7-bfb2-c115c9c4b8e5)

![Screenshot (76)](https://github.com/DSatle/RISC-V_ISA/assets/140998466/6d85eb28-f442-41db-af75-46585abb88a9)

**64 Number System for Signed Numbers**

For getting negative numbers we use concept of 2's complement which is shown in the image below.

![2's complement](https://github.com/DSatle/RISC-V_ISA/assets/140998466/2f93266b-66dc-4b65-b88d-85d90fbe436f)


Here we are devoting MSB for sign representation. 

if MSB =1; number is negative
if MSB =0; number is positive.

The image below describes the two method to convert negative binary numbers into decimal numbers

![Screenshot (77)](https://github.com/DSatle/RISC-V_ISA/assets/140998466/51ed6bc5-8aaa-4138-a5de-1af084a446c5)


Range for positive & negative numbers is shown below

![positive number signed range](https://github.com/DSatle/RISC-V_ISA/assets/140998466/97cd8b15-f273-4a4f-a56f-cbdc1112683d)


![range -ve numbers](https://github.com/DSatle/RISC-V_ISA/assets/140998466/c8c0b82d-f007-4b94-b078-ab8174bbb511)

**Lab for signed & unsigned numbers**


  

# Day_2 Introduction to ABI & basic verification flow

<details>
 <summary> Application Binary Interface
 </summary>

**Application Binary interface**

Introduction to Application binary interface- The way a user can access a architeture resources through system call is called application binary interface, its also calledsystem call interface. If application programmmer wants to access the hardware resources it is done via registers.

The below image shows the different levels between user and layout. 

![Screenshot (75)](https://github.com/DSatle/RISC-V_ISA/assets/140998466/d08f4b3f-8694-4983-b7f1-c7b3b6509131)

 ![3](https://github.com/DSatle/RISC-V_ISA/assets/140998466/a0d09816-9ab4-4f0e-9f8e-42d96d01d2b5)

   In RISc-V programmer there are 32 registers & width is defined by XLEN.
  XLEN is 32 bit for RV32
  XLEN is 64 bit for RV64.

  ![registers](https://github.com/DSatle/RISC-V_ISA/assets/140998466/5abaa9e6-dacb-42a1-93d6-1ebb949448ba)


  **Memory Allocation for Double words**
  



 








