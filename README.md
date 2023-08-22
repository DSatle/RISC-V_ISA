
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

</details>
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

</details>
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
Here we will look at the range of unsigned and signed numbers.

Following is the code for highest unsigned number

```
#include <stdio.h>
#include <math.h>

int main ()
{ unsigned long long int max = (unsigned long long int) (pow(2,64) - 1);
  printf("highest number represented by unsigned long long int is %llu\n", max);
  return 0;
  }
```

To run the command I used following commands in the terminal
```
 /home/divyam/riscv_toolchain/riscv64-unknown-2019.08.0-x86_64-linux-ubuntu14/bin/riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o unsigned.o unsigned.c

 /home/divyam/riscv_toolchain/riscv64-unknown-2019.08.0-x86_64-linux-ubuntu14/bin/spike pk unsigned.o

 ```
One can observe the output in the below image

![signed highest](https://github.com/DSatle/RISC-V_ISA/assets/140998466/c65e50a7-241a-4840-87ac-de2a2cb5edc3)

For getting the lowest negative number following C code was used

```
#include <stdio.h>
#include <math.h>

int main ()
{  long long int max = ( long long int) (pow(2,64) * - 1);
  printf("highest number represented by  long long int is %lld\n", max);
  return 0;
  }
```
To run the above code following commands were used 

```
 /home/divyam/riscv_toolchain/riscv64-unknown-2019.08.0-x86_64-linux-ubuntu14/bin/riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o signed.o signed.c

 /home/divyam/riscv_toolchain/riscv64-unknown-2019.08.0-x86_64-linux-ubuntu14/bin/spike pk signed.o

 ```
The below image shows the output obtained 

![lowest](https://github.com/DSatle/RISC-V_ISA/assets/140998466/ac9daf71-e20c-4c29-a5d1-f345f7b3cfea)

Now we will look at the range of least negative and highest positive number, code for which is given below

```
#include <stdio.h>
#include <math.h>
int main() {
long long int max = (int) (pow(2,63) -1);
long long int min = (int) (pow(2,63) * -1);
printf("highest number represented by long long int is %lld\n", max);
printf("lowest number represented by long long int is %lld\n", min);
return 0;
```
Here we can see the range is not correct.
 
![both](https://github.com/DSatle/RISC-V_ISA/assets/140998466/7390fe59-a273-4053-b7c7-5853229f7e1c)

The correct code and output is given below 
```
#include <stdio.h>
#include <math.h>
int main() {
long long int max = (long long int) (pow(2,63) -1);
long long int min = (long long int) (pow(2,63) * -1);

printf("highest number represented by long long int is %lld\n", max);
printf("lowest number represented by long long int is %lld\n", min);
return 0;
}
```

![both_modify](https://github.com/DSatle/RISC-V_ISA/assets/140998466/ed2f25bd-5dd4-4e01-af71-9353ca2e72ab)


  </details>

# Day_2 Introduction to ABI & basic verification flow
</details>
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

RISC-V has 32 64-bit registers. There are two ways in which data can be loaded to the register.

1. Direct loading- In this method data is directly loaded to the register. The below image shows the method

![1](https://github.com/DSatle/RISC-V_ISA/assets/140998466/f377ea41-f1c8-4bf1-a019-0e91ee99dbba)

2. Via memory- Since we have limited registers in RISC-V the data is first stored in the memory this data is then transfered to registers. The below image show the method.

![2](https://github.com/DSatle/RISC-V_ISA/assets/140998466/81fad43b-71f7-498b-b975-9579d5a1c9d5)

Little endian method- The RISC-V uses the little endian approach to fill the data in the memory i.e. the data from LSB gets start filling in the memory, from bottom to top respectively. A pictorial presentation of which is shown in the image below.

![4](https://github.com/DSatle/RISC-V_ISA/assets/140998466/a01b147b-8719-4b53-aeeb-22452b2bbf3e)


  **Load,Add and Store Instructions with examples**
  
Here I came to know about the how data is transfered from memory to register and add operation on the data and then transfer of data from register to memory.
Following commands were used to do the above operations.
```
ld x8, 16(x23) // ld stands from load. Initially the pointer is at 0. Since the data is at 16th location the register x23 will go to 16th location and load that 
                  data to into x8. x8 is destination register and x23 is source register.

add x8, x24,x8  // here the data of x8 and x24 is added and then finally stored in x8.

sd x8, 8(x23)  // here the data from x23 register is stored to the memory location starting from 8.

```
The whole process discussed above is shown in the below two images.

![4](https://github.com/DSatle/RISC-V_ISA/assets/140998466/a663265a-20cb-4c2c-b378-a637c3d75575)

![8](https://github.com/DSatle/RISC-V_ISA/assets/140998466/e3d22e95-5e3c-4a17-bd26-4524951c9eab)

The above picture also describes which bits are indicate which part of the assembly level language. Every instruction in RISC-V is 32 bit.

  **Concluding 32-registers And their respective ABI names**

There are following type of instructions 
1. R-type:- These instructions operate on registers.
  
2. I-type:- These instructions consists immediate in it and operates on registers.

3. S-type:- Instructions that consists store in it.
    
 ![8](https://github.com/DSatle/RISC-V_ISA/assets/140998466/43bf8f6b-f383-4d00-ba79-c679d741f688)

 As we can observe there are 5 bits dedicated for register in the machine level code. As 2^5= 32 this the logic behind having 32 registers in the RISC-V architeture.
 
 The RISC-V instructions are bifurgated in following types shown in the table below.

 ![9](https://github.com/DSatle/RISC-V_ISA/assets/140998466/de382f85-93af-41f2-b5f6-a76247864577)
 
</details>
 <details>
 <summary> Labwork using ABI function calls
 </summary>
  
**Study New Algorithm For Sum 1 to N using ASM**
Here we are going to apply the knowledge of instructions which we got familiar in the previous tutorial. Here we are going to push some functionalities from C program to assembly language program. And get fetch the end result from assembly level program to the C program. A pictorial view of the above mention method is shown below.

![basic working](https://github.com/DSatle/RISC-V_ISA/assets/140998466/03942c58-975a-4c6d-8b57-45b8a4e8651c)

To apply this method we are going to follow the below algorithm shown in the picture 

![algorithm](https://github.com/DSatle/RISC-V_ISA/assets/140998466/0385b71f-f191-4281-adeb-b9371623e220)

**Review ASM Function call**
Here I have modified my C code inorder to implement the method discussed above in the previous section, the modified C code is given below.

```
#include <stdio.h>

extern int load(int x, int y);

int main ()
{
   int result = 0;
   int count = 9;
   result = load(0x0, count+1);
   printf ("Sum of number from 1 to %d is %d\n", count, result);
   }
```
Here I have written assembly level program as well inorder to execute the algorithm the code for which is given below

```
.section .text
.global load
.type load, @function

load: 
        add      a4, a0, zero //Initialize sum register a4 with 0x0
        add      a2, a0, a1   //store count of 10 in register a2.Register a1 is loaded with 0xa (decimal 10) from main
        add      a3, a0, zero //initialize intermediate sum register a3 by 0
loop:   add      a4, a3, a4 //Incremental addition
        addi     a3, a3, 1 //Increment intermediate register by 1
        blt      a3, a2, loop //If a3 is less than a2, branch to label named <loop>
        add      a0, a4, zero //Store final result to register a0 so that it can be read by main program
        ret 
```

**Simulate New C Program With Function Call**
Here I run the modified codes of C as well as the assembly langguage. The commands are similar to the ones used before one can observe them in the images below.

![1](https://github.com/DSatle/RISC-V_ISA/assets/140998466/97454088-7c58-427d-aced-5cf2ff6d4546)

![2](https://github.com/DSatle/RISC-V_ISA/assets/140998466/854e0764-ead7-469e-8eaf-a111f08037ba)

![3](https://github.com/DSatle/RISC-V_ISA/assets/140998466/443e1d14-8167-4356-a4d2-154230de0f65)

![4](https://github.com/DSatle/RISC-V_ISA/assets/140998466/989b7773-558d-455c-9ba8-9360a1461fa6)

**Lab to run C program on RISC-V CPU**

Here we have a RISC-V CPU written in verilog & we will create a testbench. Then we will read the hex format C program through RISC-V CPU & output will be displayed.The whole process is described below. 

![10](https://github.com/DSatle/RISC-V_ISA/assets/140998466/c7097815-4bed-4020-8d12-1d3ee6280151)

To run the program in the terminal using following commands.

```
chmod 777 rv32im.sh
./rv32im..sh
```
The image below shows the output displayed in ubuntu terminal.

![11](https://github.com/DSatle/RISC-V_ISA/assets/140998466/234673fb-3b96-4664-8b47-8a2bb4082bdd)

</details>

# Day_3 Digital Logic with TL-verilog & makerchip
</details>
<details>
 <summary> Combinational Logic in TL-verilog using Makerchip.
 </summary>

**Introduction to Logic gates**

Logic gates are the fundamental basic building blocks

![gates](https://github.com/DSatle/RISC-V_ISA/assets/140998466/69098693-8328-4530-af8c-1b69b93c9477)


As logic gates are the basic building blocks of a circuit. Here I learned how I can implement the logic gates using TL-verilog. The table below describes respective code for the logic gates.

![Logic gates verilog](https://github.com/DSatle/RISC-V_ISA/assets/140998466/f28afd6a-2279-4499-b608-105b839f511f)

A full adder circuit madeup of logic gates.

![adder](https://github.com/DSatle/RISC-V_ISA/assets/140998466/9512c8ab-5f55-45dc-a1af-3a0ccc4ecc7c)

A adder circuit made using logic gates.

![carr](https://github.com/DSatle/RISC-V_ISA/assets/140998466/36706a16-736b-42d6-bc12-04d334e360d0)

**Basic Mux implementation & Introduction to makerchip**

Basic mux 2x1 is made using the following commands, here we are using ternary operator which is similar to if statement in C program.

```
assign f = s ? x1 : x2;
```

![2x1 mux](https://github.com/DSatle/RISC-V_ISA/assets/140998466/bc71ba8e-f9b5-421a-b059-562b21cad1c1)

The below image shows the 4x1 mux implemented using 2x1 mux and verilog code for that as well

![4x1 mux](https://github.com/DSatle/RISC-V_ISA/assets/140998466/309613c3-c49c-4802-9915-ab6232ed4024)

Introduction to makerchip

1. Type maker chip in tab of your search engine & launch Makerchip IDE.
2. Go to Learn, click on Examples and select FPGA multipler.

![MakerChip tutorial](https://github.com/DSatle/RISC-V_ISA/assets/140998466/bbdafb04-4dda-4251-b153-5c53daacc280)

Inverter Gate on makerchip

![Inverter](https://github.com/DSatle/RISC-V_ISA/assets/140998466/87b47c86-9ba2-4700-860d-293ce1714d94)

Vector of 5 bits

![vector](https://github.com/DSatle/RISC-V_ISA/assets/140998466/8852e1e5-f21b-4a76-a1a0-596a2cbc9303)

Mux with single bit 

![mux made me](https://github.com/DSatle/RISC-V_ISA/assets/140998466/0a946c60-5e10-414b-8e44-eef042a7f5e4)

Mux with vector input

![mux vector](https://github.com/DSatle/RISC-V_ISA/assets/140998466/7c25157d-cec2-475a-8651-0dc5752fa589)

Combinational Calculator

![calculator](https://github.com/DSatle/RISC-V_ISA/assets/140998466/b3d745ee-8992-4ef9-9c42-1a3ded4f498c)
</details>
<details>
 <summary> Sequential Logic
 </summary>
 
**Introduction to sequntial logic & counter lab**

Sequential Circuit essentially consists a clock over combinational circuit. The value transition takes place on either positive or negative edge of the clock.
The below image describes the basic idea of sequential circuit.

![basic seq  circuit](https://github.com/DSatle/RISC-V_ISA/assets/140998466/c2c859fd-c5c2-4449-be8b-2eec869705f2)

Fibonacci Series 

The below image gives an idea how the circuit for performing Fibonacci series is implemented.

![fibbonacci series ckt and waveform](https://github.com/DSatle/RISC-V_ISA/assets/140998466/731ab09b-e976-42e8-b0e1-77bda3d443dd)


Free Running counter 

The below image show code and working of a free running counter designed using sequential circuit, one can observe the importance of clock in the circuit as the output changes only for positive clock.

![Counter circuit](https://github.com/DSatle/RISC-V_ISA/assets/140998466/0032964a-c017-417d-9aa3-dc2fb5b82bb9)

The basic circuit block diagram is given below

![count ckt](https://github.com/DSatle/RISC-V_ISA/assets/140998466/cc25d985-e178-4b86-830c-27d0bd4209a0)

**Sequential calculator lab**

![seq  calculator](https://github.com/DSatle/RISC-V_ISA/assets/140998466/36422d30-878d-40e9-bb3b-8ea79f8dd89c)


</details>
<details>
 <summary> Pipeline Logic
 </summary>

**Pipelined logic & retiming**

The concept of pipeling is explained using the Pythagoras theorem.

Basics of pythagoras theorem on makerchip

![pytha](https://github.com/DSatle/RISC-V_ISA/assets/140998466/d696a4d0-2d07-4908-a151-869fa08781a6)

TL-verilog gives the ability to model the process in timing abstract representation. The basic idea of pipelining is to break the whole process in different stages. The below image shows the use of pipelining concept in TL-verilog compared to other RTL languages.

![rtl vs tl-verilog](https://github.com/DSatle/RISC-V_ISA/assets/140998466/f44d8c55-edf8-4a11-8981-79a0fd9b24d2)

Timing abstract gives the advantage to manipulate pipelining & its stages. i.e staging is a physical attribute it has no impact on behaviour as shown in the below image

![remtiming ](https://github.com/DSatle/RISC-V_ISA/assets/140998466/aaa1ce9e-a09f-4f6f-8f72-d4401ad36892)


The below image show the code for pipelining in TL-verilog.

![tl verilog code](https://github.com/DSatle/RISC-V_ISA/assets/140998466/ff95517b-f066-4b1f-b7e2-38ec95bbce57)

Image shows comparison of code between system verilog and TL-verilog.

![s vl vs tlvl](https://github.com/DSatle/RISC-V_ISA/assets/140998466/f9d7d47e-b40f-48e4-a5ab-e07db0721a36)

**Pipeline logic advantages and demo in platform**

1. By applying pipelining we are able to run our clock at higher speed.
2. In diagram 2, one can observe that we can introduce new input at every clock cycle. So we can introduce more inputs using pipeline.

![basic idea of pipelining](https://github.com/DSatle/RISC-V_ISA/assets/140998466/888ebeae-1036-4ed8-9268-88f0f47d08dd)

Here we will understand the minute details of pipelining concept.

Here in the below image one can observe that there is single stage pipeline, so the output for C comes at the same stage.

![pytha single pipeline](https://github.com/DSatle/RISC-V_ISA/assets/140998466/44147a9e-4e59-4a9a-a8ad-ff8138d73017)

Now when we change the single stage pipeline to 3 stage pipeline, now the output C comes 2 stage later than a & b. This can be observed in the below image.

![pipelining pytha 3step](https://github.com/DSatle/RISC-V_ISA/assets/140998466/56f686fd-237c-4b5f-b5fc-50ee4d6f044d)

At last here we are seeing the concept of feedback how varying the no. of feedback stages in code gets reflected in the diagram of pipeline. Here in the code we have set the code for 4 stage feedback which can be observed in the diagram as well.

![feedback concept](https://github.com/DSatle/RISC-V_ISA/assets/140998466/11d373c7-3f7e-4a32-8f7a-191336183ad9)

**Lab on Error Conditions within Computation Pipeline**

**Classification** 

**Pipe Signal**- All the instuctions are written in lower case. e.g.-$lower_case

**Pascal case/State Signal** - In this the first letter of both terms is written in upper case. eg.- $CamelCase

**Keyword Signal** - All the letters in the instructions are written in upper case. e.g.- $UPPER_CASE.

**Numbers end tokens** - $base64_value-- This was is considered as a good practice in TL-Verilog.
                         $bad_name_5 -- This is avoidable practice in TL--Verilog

 **Numeric identifiers**- e.g. >>1 this instruction indicates ahead by 1.

 For pipelining of error I used following code in makerchip

 ```
 $reset = *reset;
   |comp 
      @1
         $err1 = $bad_input || $illegal_op;
      @2 
         $err2 = $err1 || $overflow;
      @3
         $err3 = $err2 || $div_by_zero;

```

The following picture shows the output

![error ip](https://github.com/DSatle/RISC-V_ISA/assets/140998466/884d951c-c137-428d-abe4-adcf19737b71)

![asked](https://github.com/DSatle/RISC-V_ISA/assets/140998466/60789cd3-2250-4440-a37e-40f234721e5c)


**Lab on 2-Cycle Calculator**

Value Representation in Verilog 

The below image show how numbers are represnted in verilog.

![value representation](https://github.com/DSatle/RISC-V_ISA/assets/140998466/5fb0597c-cba2-4209-8a23-5fa6400aae42)


</details>

</details>
<details>
 <summary> Validity
 </summary>

**Validity** is a notion for when the values or the signals are meaningful.
Validity provides

* Easier Debug 
* Cleaner Design
* Better error checking
* Automated Clock gating

Let us implement the Pythagoran's theorem with validity:

![validity pythagoran](https://github.com/DSatle/RISC-V_ISA/assets/140998466/ecebb6f8-6333-4115-abcc-b8c5205536ff)

**Clock Gating** is a power-saving property.
* Motivation
  
  1.1 Clock signals are distributed to EVERY flipflop.
  
  1.2 Clocks toggle twice per cycle.
  
  1.3 This consumes power.
  
* Clock gating avoids toggling clock signals.
* 
* TL-verilog can produce fine-grained gating (or enables).

**LAB**- Distance Accumulator with Pythagoran's theorem.

![validity pythagoran](https://github.com/DSatle/RISC-V_ISA/assets/140998466/5ad3408c-1102-4397-8606-c0aef83e6aed)

**LAB**- Cycle calculator with Validity
The pipeline structure is 

![validity pythagoran](https://github.com/DSatle/RISC-V_ISA/assets/140998466/db01e1ce-d7c6-4488-9a3d-8d97f31d926a)

The makerchip implementation output:

![cycle calculator makerchip](https://github.com/DSatle/RISC-V_ISA/assets/140998466/e3162aca-92dd-4b68-b182-b38e95d01777)

**LAB**- Calculator with single value Memory

The pipeline str. is as follows

![single memory strc](https://github.com/DSatle/RISC-V_ISA/assets/140998466/68a3888c-def0-42e6-8c0b-f7bceda3e13f)

Makerchip Implementation

![single memory strc](https://github.com/DSatle/RISC-V_ISA/assets/140998466/7150e820-dd69-4703-9b95-88bb25ebdc73)

</details>

</details>
<details>
 <summary> Wrap-UP
 </summary>

**LAB** - conway's game of life:

![Conway game of life](https://github.com/DSatle/RISC-V_ISA/assets/140998466/3563e237-7e44-4d64-910b-36be9088c836)

**LAB** - Pythagoran's theorem:

![pytha str](https://github.com/DSatle/RISC-V_ISA/assets/140998466/3d2ff0af-2021-43cf-baa5-f13a9dfd058c)

The makerchip output:

![makerchip implementation](https://github.com/DSatle/RISC-V_ISA/assets/140998466/4d050a11-f0cd-4b74-b4d2-8c46d3e991ba)

</details>

## Day_4 Basic RISC-V CPU Archituecture

</details>
<details>
 <summary> Introduction to Simple RISC-V Microarchiteture
 </summary>
 
The micro architecture for the RISC-V implementation is shown here:

![1](https://github.com/DSatle/RISC-V_ISA/assets/140998466/15b5cf57-5aee-49de-b313-25fc59535fa9)


**Basic terminologies**

**Program counter** - The Program counter is a pointer to the instruction memory as to which instrcution must be executed next.

**Decoder** - The Decoder interprets the instruction and send signals regarding the action of the processor and the location of data. The decoder also sends incremented by 1 value to the PC, instructing it to move to the next instruction.

**Register Files** - These implements the read and write operations on the data/memory.

**ALU** - ALU computes the arithmetic operations and write the result back to the register file.

</details>

</details>
<details>
 <summary> Fetch & Decode 
 </summary>

 
 The implementation plan of RISC-V CPU Core:

 ![2](https://github.com/DSatle/RISC-V_ISA/assets/140998466/c18e68da-5e00-43ee-9463-221273d6e1f6)


 **LAB - PC:**

 The implementation pipeline

 ![3](https://github.com/DSatle/RISC-V_ISA/assets/140998466/74b74393-a07e-4f3a-b3ae-07e9c673bd7c)

 The makerchip output 

 ![4](https://github.com/DSatle/RISC-V_ISA/assets/140998466/9143eaf8-2d7c-449a-812d-49f5dce2c160)

 **LAB - FETCH**
The pipeline structure(part-1):

![6](https://github.com/DSatle/RISC-V_ISA/assets/140998466/058f581b-2b55-4d59-a6f2-41c971a4487d)

The pipeline structure(part-2): 

![7](https://github.com/DSatle/RISC-V_ISA/assets/140998466/8bef874e-b466-4ac1-9346-3e3f842d1007)

The makerchip implementation output:

![8](https://github.com/DSatle/RISC-V_ISA/assets/140998466/f5453a39-1891-4f12-84a8-896f383846fe)

**LAB - INSTRUCTION TYPE DECODE**

The Pipeline Structure 

![9](https://github.com/DSatle/RISC-V_ISA/assets/140998466/e89f7b44-11cd-42a4-9ca5-6a3f6376de1e)

The makechip output 

![10](https://github.com/DSatle/RISC-V_ISA/assets/140998466/d19e50ee-4613-44a4-a27d-6a3b35754f1e)

**LAB - INSTRUCTION IMMEDIATE DECODE**

![11](https://github.com/DSatle/RISC-V_ISA/assets/140998466/e1d4ad68-0a27-4786-b46b-48f9da516a95)

The implementation output:

![12](https://github.com/DSatle/RISC-V_ISA/assets/140998466/f42a0d27-6830-44f4-93f3-74d9cc45f125)

**LAB - INSTRUCTION FIELD DECODE**

![13](https://github.com/DSatle/RISC-V_ISA/assets/140998466/7974f6be-ed46-4145-aecf-b7a36ecf0983)

The implementation output:

![14](https://github.com/DSatle/RISC-V_ISA/assets/140998466/04ab3039-751e-4799-aeb8-40e84431fbe9)

**LAB - INSTRUCTION DECODE_2**

![15](https://github.com/DSatle/RISC-V_ISA/assets/140998466/3d608530-9f4b-47f4-bb56-525a7816fe0a)

The implementation output:

![16](https://github.com/DSatle/RISC-V_ISA/assets/140998466/c62fb75a-f8cb-4a5e-902f-3059fbe89a56)

</details>
<details>
 <summary> RISC-V control logic
 </summary>

 **LAB - REGISTER FILE READ_1**

The pipeline structure is as follows

 ![17](https://github.com/DSatle/RISC-V_ISA/assets/140998466/30da51b2-27d1-4399-bf94-e3fda75c41fa)

![18](https://github.com/DSatle/RISC-V_ISA/assets/140998466/93e145f2-371e-4538-b4ae-6edf26d78a3a)

**LAB - REGISTER FILE READ_2**

The pipeline structure:

![19](https://github.com/DSatle/RISC-V_ISA/assets/140998466/dda3e0bf-d434-442c-a7af-8271871331a7)

The makerchip implementation output:

![20](https://github.com/DSatle/RISC-V_ISA/assets/140998466/80408f05-8c78-4bcb-80aa-d5646d692160)

**LAB - ALU**

The pipeline structure 

![22](https://github.com/DSatle/RISC-V_ISA/assets/140998466/503e4cfa-970c-4f45-9229-1f27d58b27fe)

The implementation output

![22](https://github.com/DSatle/RISC-V_ISA/assets/140998466/ab56f695-f021-4131-b0a0-7fc420f62be6)

LAB - REGISTER FILE WRITE

![23](https://github.com/DSatle/RISC-V_ISA/assets/140998466/ea2db25a-2f23-4555-b03a-c064bec42e23)

The makerchip implementation output:

![24](https://github.com/DSatle/RISC-V_ISA/assets/140998466/a36942dc-59d6-4549-9804-f3bbd41c6be0)

**Arrays**

![25](https://github.com/DSatle/RISC-V_ISA/assets/140998466/cddec658-00e2-40fa-b695-bb19c539e524)

The detailed implementation of Register files is given below:

![26](https://github.com/DSatle/RISC-V_ISA/assets/140998466/8b928844-96a4-4f38-93ee-a18b15ab6175)

The implementation output:

![27](https://github.com/DSatle/RISC-V_ISA/assets/140998466/b8b88886-8093-4983-af58-3b3c78ad64b9)

![28](https://github.com/DSatle/RISC-V_ISA/assets/140998466/7a88a029-1c6e-4e35-97dd-887953a4a998)

The output is shown in the image below

![30](https://github.com/DSatle/RISC-V_ISA/assets/140998466/85159322-825b-441e-811f-160083fe1c0f)

**LAB- Test bench**

The makerchip implementation output is as shown below:-

![31](https://github.com/DSatle/RISC-V_ISA/assets/140998466/ae2b468b-758e-45b9-abd3-699671420e7c)

</details>

## Day_5 Complete Pipelined RISC-V CPU micro-architecture

</details>
<details>
 <summary> Pipelining the CPU
 </summary>

![1](https://github.com/DSatle/RISC-V_ISA/assets/140998466/9099d51f-0b19-4cd4-a710-8aac61f78686)

**LAB - 3-CYCLE VALID SIGNAL**

The implementation output is:

![2](https://github.com/DSatle/RISC-V_ISA/assets/140998466/62a9e575-5f2a-4f88-9d71-8096672111fd)

**LAB - CYCLE RISC-V**

![3](https://github.com/DSatle/RISC-V_ISA/assets/140998466/adc22d70-cba5-46eb-bbcb-ae3345147847)

The implementation output is shown below

![4](https://github.com/DSatle/RISC-V_ISA/assets/140998466/d04d6e72-68fe-4552-94d1-96eacd8e957d)

</details>


</details>
<details>
 <summary> Solutions to Pipeline Hazards
 </summary>

 **REGISTER FILE BYPASS**

 The pipeline structure is as follows

![5](https://github.com/DSatle/RISC-V_ISA/assets/140998466/361b1a20-7642-4f94-9545-89dcef490a3f)

The implementation output is shown below in the image

![6](https://github.com/DSatle/RISC-V_ISA/assets/140998466/062d231a-756e-4666-82dd-dd7768732ad9)

**LAB - BRANCHES**

![7](https://github.com/DSatle/RISC-V_ISA/assets/140998466/3e0c2099-ced7-40f7-874f-d0cdc9ed2dc1)

The implemented output is shown below

![8](https://github.com/DSatle/RISC-V_ISA/assets/140998466/cf22e9d1-1612-41ec-8dec-7a12b88f3494)

**LAB-ALU**

The makerchip implementation results are:

![9](https://github.com/DSatle/RISC-V_ISA/assets/140998466/463e4c7d-f46e-476f-b05b-4f69de33396e)

</details>


</details>
<details>
 <summary> Load/Store Instructions and Completing RISC-V CPU
 </summary>

**LOAD**

The pipeline structure 

![10](https://github.com/DSatle/RISC-V_ISA/assets/140998466/781d3d42-8770-44a1-9b9b-d52f3e4b7d52)

The implementation output:

![11](https://github.com/DSatle/RISC-V_ISA/assets/140998466/87536abd-0d76-4e3f-ba9b-cd404c72819b)

**LOAD/STORE**

![12](https://github.com/DSatle/RISC-V_ISA/assets/140998466/074fbfc1-0eb3-4084-9a84-dc9d108710b9)

The implementation output

![13](https://github.com/DSatle/RISC-V_ISA/assets/140998466/cef44fc2-7ce3-4b8e-832a-420ad33bfa5b)

**JUMPS**

![14](https://github.com/DSatle/RISC-V_ISA/assets/140998466/938118f8-48a8-44fd-9a8c-beaac3b0c107)

The makerchip output:

![15](https://github.com/DSatle/RISC-V_ISA/assets/140998466/c3dd16f9-56da-46f1-b1d3-d9077072894f)

**RISC-V CORE CPU - FINAL IMPLEMENTATION**

The RISC-V final code is shown below:

```
\m4_TLV_version 1d: tl-x.org
\SV
   // This code can be found in: https://github.com/stevehoover/RISC-V_MYTH_Workshop
   
   m4_include_lib(['https://raw.githubusercontent.com/Lasya-G/Risc_V/main/risc-v_shell_lib.tlv'])

\SV
   m4_makerchip_module   // (Expanded in Nav-TLV pane.)
\TLV

   // /====================\
   // | Sum 1 to 9 Program |
   // \====================/
   //
   // Program for MYTH Workshop to test RV32I
   // Add 1,2,3,...,9 (in that order).
   //
   // Regs:
   //  r10 (a0): In: 0, Out: final sum
   //  r12 (a2): 10
   //  r13 (a3): 1..10
   //  r14 (a4): Sum
   //
   // External to function:
   m4_asm(ADD, r10, r0, r0)             // Initialize r10 (a0) to 0.
   // Function:
   m4_asm(ADD, r14, r10, r0)            // Initialize sum register a4 with 0x0
   m4_asm(ADDI, r12, r10, 1010)         // Store count of 10 in register a2.
   m4_asm(ADD, r13, r10, r0)            // Initialize intermediate sum register a3 with 0
   // Loop:
   m4_asm(ADD, r14, r13, r14)           // Incremental addition
   m4_asm(ADDI, r13, r13, 1)            // Increment intermediate register by 1
   m4_asm(BLT, r13, r12, 1111111111000) // If a3 is less than a2, branch to label named <loop>
   m4_asm(ADD, r10, r14, r0)            // Store final result to register a0 so that it can be read by main program
   m4_asm(SW, r0, r10, 10000)           // Store the final result value to byte address 16
   m4_asm(LW, r15, r0, 10000)           // Load the final result value from adress 16 to x17
   
   // Optional:
   // m4_asm(JAL, r7, 00000000000000000000) // Done. Jump to itself (infinite loop). (Up to 20-bit signed immediate plus implicit 0 bit (unlike JALR) provides byte address; last immediate bit should also be 0)
   m4_define_hier(['M4_IMEM'], M4_NUM_INSTRS)


   |cpu
      @0
         $reset = *reset;
         
         //MODIFIED NEXT PC LOGIC FOR INCLUDING BRANCH INSTRCUTIONS
         $pc[31:0] = >>1$reset ? 32'b0 :
                     >>3$valid_taken_branch ? >>3$br_target_pc :
                     >>3$valid_load ? >>3$inc_pc :
                     >>3$valid_jump && >>3$is_jal ? >>3$br_target_pc :
                     >>3$valid_jump && >>3$is_jalr ? >>3$jalr_target_pc :
                     >>1$inc_pc ;
         //START LOGIC TO PROVIDE FIRST VALID LOGIC
         //$start = (>>1$reset && $reset == 0) ? 1'b1 : 1'b0;
         //$valid = $reset ? 1'b0 :
                  //$start ? 1'b1 : >>3$valid;
     
      @1  
         //INSTRUCTION FETCH
         $inc_pc[31:0] = $pc + 32'd4;
         
         $imem_rd_en = !$reset;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         
         $instr[31:0] = $imem_rd_data[31:0];
         
         //INSTRUCTION TYPES DECODE        
         
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         
         $is_r_instr = $instr[6:2] ==? 5'b011x0 ||
                       $instr[6:2] ==? 5'b01011 ||
                       $instr[6:2] ==? 5'b10100;
         
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                       $instr[6:2] ==? 5'b001x0 ||
                       $instr[6:2] ==? 5'b11001;
         
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         
         //INSTRUCTION IMMEDIATE DECODE
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                      $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                      $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                      $is_u_instr ? {$instr[31:12], 12'b0} :
                      $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                                                            32'b0;
         //INSTRUCTION DECODE
         $opcode[6:0] = $instr[6:0];
         
         
         //INSTRUCTION FIELD DECODE
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
           
         $rs1_valid = $is_r_instr  || $is_s_instr || $is_b_instr || $is_i_instr;
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         
         $funct3_valid = $is_r_instr  || $is_s_instr || $is_b_instr || $is_i_instr;
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
           
         $funct7_valid = $is_r_instr ;
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
           
         $rd_valid = $is_r_instr  || $is_u_instr || $is_j_instr || $is_i_instr;
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         
         
      @2
         //INSTRUCTION DECODE
         $dec_bits[10:0] = {$funct7[5],$funct3,$opcode};
         $is_beq = $dec_bits ==? 11'bx_000_1100011;
         $is_bne = $dec_bits ==? 11'bx_001_1100011;
         $is_blt = $dec_bits ==? 11'bx_100_1100011;
         $is_bge = $dec_bits ==? 11'bx_101_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         $is_add = $dec_bits ==? 11'b0_000_0110011;
         $is_lui = $dec_bits ==? 11'bx_xxx_0110111;
         $is_auipc = $dec_bits ==? 11'bx_xxx_0010111;
         $is_jal = $dec_bits ==? 11'bx_xxx_1101111;
         $is_jalr = $dec_bits ==? 11'bx_000_1100111;
         $is_load = $opcode == 7'b0000011;
         $is_sb = $dec_bits ==? 11'bx_000_0100011;
         $is_sh = $dec_bits ==? 11'bx_001_0100011;
         $is_sw = $dec_bits ==? 11'bx_010_0100011;
         $is_slti = $dec_bits ==? 11'bx_010_0010011;
         $is_sltiu = $dec_bits ==? 11'bx_011_0100011;
         $is_xori = $dec_bits ==? 11'bx_100_0100011;
         $is_ori = $dec_bits ==? 11'bx_110_0100011;
         $is_andi = $dec_bits ==? 11'bx_111_0100011;
         $is_slli = $dec_bits ==? 11'b0_001_0100011;
         $is_srli = $dec_bits ==? 11'b0_101_0100011;
         $is_srai = $dec_bits ==? 11'b1_101_0100011;
         $is_sub = $dec_bits ==? 11'b1_000_0110011;
         $is_sll = $dec_bits ==? 11'b0_001_0110011;
         $is_slt = $dec_bits ==? 11'b0_010_0110011;
         $is_sltu = $dec_bits ==? 11'b0_011_0110011;
         $is_xor = $dec_bits ==? 11'b0_100_0110011;
         $is_srl = $dec_bits ==? 11'b0_101_0110011;
         $is_sra = $dec_bits ==? 11'b1_101_0110011;
         $is_or = $dec_bits ==? 11'b0_110_0110011;
         $is_and = $dec_bits ==? 11'b0_111_0110011;
         
         $jalr_target_pc[31:0] = $src1_value +$imm ;
      @3
         $is_jump = $is_jal || $is_jalr ;   
         `BOGUS_USE($is_beq $is_bne $is_blt $is_bge $is_bltu $is_bgeu $is_addi $is_add
                    $is_lui $is_auipc $is_jal $is_jalr $is_load $is_sb $is_sh $is_sw $is_slti
                    $is_sltiu $is_xori $is_ori $is_andi $is_slli $is_srli $is_srai $is_sub $is_sll
                    $is_slt $is_sltu $is_xor $is_srl $is_sra $is_or $is_and)
         
      @2  
         //REGISTER FILE READ
         //$rf_wr_en = 1'b0;
         //$rf_wr_index[4:0] = 5'b0;
         //$rf_wr_data[31:0] = 32'b0;
         $rf_rd_en1 = $rs1_valid;
         $rf_rd_index1[4:0] = $rs1;
         $rf_rd_en2 = $rs2_valid;
         $rf_rd_index2[4:0] = $rs2;
         
         $src1_value[31:0] = >>1$rf_wr_en && (>>1$rf_wr_index == $rf_rd_index1) ? >>1$result : $rf_rd_data1;
         $src2_value[31:0] = >>1$rf_wr_en && (>>1$rf_wr_index == $rf_rd_index2) ? >>1$result : $rf_rd_data2;
         $br_target_pc[31:0] = $pc +$imm;
         
      @3  
         //ARITHMETIC AND LOGIC UNIT (ALU)
         
         $sltu_rslt[31:0] = $src1_value < $src2_value;
         $sltiu_rslt[31:0] = $src1_value < $imm;
         $result[31:0] = $is_addi ? $src1_value + $imm :
                         $is_add ? $src1_value + $src2_value :
                         $is_andi ? $src1_value & $imm :
                         $is_ori ? $src1_value | $imm :
                         $is_xori ? $src1_value ^ $imm :
                         $is_slli ? $src1_value << $imm[5:0] :
                         ($is_addi || $is_load || $is_s_instr) ? $src1_value + $imm :
                         $is_srli ? $src1_value >> $imm[5:0] :
                         $is_and ? $src1_value & $src2_value :
                         $is_or ? $src1_value | $src2_value :
                         $is_xor ? $src1_value ^ $src2_value :
                         $is_sub ? $src1_value - $src2_value :
                         $is_sll ? $src1_value << $src2_value[4:0] :
                         $is_srl ? $src1_value >> $src2_value[4:0] :
                         $is_sltu ? $sltu_rslt :
                         $is_sltiu ? $sltiu_rslt :
                         $is_lui ? {$imm[31:12],12'b0} :
                         $is_auipc ? $pc + $imm :
                         $is_jal ? $pc + 4 :
                         $is_jalr ? $pc + 4 :
                         $is_srai ? { {32{$src1_value[31]}},$src1_value} >> $imm[4:0] :
                         $is_slt ? ($src1_value[31] == $src2_value[31]) ? $sltu_rslt : {31'b0,$src1_value[31]} :
                         $is_slti ? ($src1_value[31] == $imm[31]) ? $sltiu_rslt : {31'b0,$src1_value[31]} :
                         $is_sra ? { {32{$src1_value[31]}},$src1_value} >> $src2_value[4:0] :
                         32'bx;
         
         
         //REGISTER FILE WRITE
         $rf_wr_en = ($rd_valid && $rd != 5'b0 && $valid) || >>2$valid_load;
         $rf_wr_index[4:0] = >>2$valid_load ? >>2$rd : $rd;
         $rf_wr_data[31:0] = >>2$valid_load ? >>2$ld_data : $result;
         
         
         //BRANCH INSTRUCTIONS 1
         $taken_branch = $is_beq ? ($src1_value == $src2_value):
                         $is_bne ? ($src1_value != $src2_value):
                         $is_blt ? (($src1_value < $src2_value) ^ ($src1_value[31] != $src2_value[31])):
                         $is_bge ? (($src1_value >= $src2_value) ^ ($src1_value[31] != $src2_value[31])):
                         $is_bltu ? ($src1_value < $src2_value):
                         $is_bgeu ? ($src1_value >= $src2_value):
                         1'b0;
          //CYCLE VALID INSTRUCTIONS
         $valid = !(>>1$valid_taken_branch || >>2$valid_taken_branch ||
                    >>1$valid_load || >>2$valid_load) ;
         
         $valid_load = $valid && $is_load ;
         //$valid = !(>>1$valid_taken_branch || >>2$valid_taken_branch);
         $valid_taken_branch = $valid && $taken_branch;
         $valid_jump = $is_jump && $valid ;
         `BOGUS_USE($taken_branch)
      @4
         //MINI 1-R/W MEMORY
         $dmem_wr_en = $is_s_instr && $valid ;
         $dmem_addr[3:0] = $result[5:2] ;
         $dmem_wr_data[31:0] = $src2_value ;
         $dmem_rd_en = $is_load ;
         
      @5
         //LOAD DATA
         $ld_data[31:0] = $dmem_rd_data ;   
         
         
         

      // Note: Because of the magic we are using for visualisation, if visualisation is enabled below,
      //       be sure to avoid having unassigned signals (which you might be using for random inputs)
      //       other than those specifically expected in the labs. You'll get strange errors for these.

   
   // Assert these to end simulation (before Makerchip cycle limit).
   //*passed = *cyc_cnt > 40;
   *passed = |cpu/xreg[15]>>5$value == (1+2+3+4+5+6+7+8+9) ;
   *failed = 1'b0;
   
   // Macro instantiations for:
   //  o instruction memory
   //  o register file
   //  o data memory
   //  o CPU visualization
   |cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@2, @3)  // Args: (read stage, write stage) - if equal, no register bypass is required
      m4+dmem(@4)    // Args: (read/write stage)
   
   m4+viz(@4)    // For visualisation, argument should be at least equal to the last stage of CPU logic
   //@4 would work for all lab
\SV
   endmodule
```

![16](https://github.com/DSatle/RISC-V_ISA/assets/140998466/95132f97-00b9-48e8-8691-8bcc8c713312)

</details>

**Word Of Thanks**

I am thankful to Kunal Ghosh ( cofounder & CEO VSD) for providing me good quality content & resources and guiding me through out the workshop. I would also like to thank Steeve Hoover (founder of Redwood EDA), for making me understand concepts of TL-Verilog and how to implement those on makerchip.

**References**

1. https://www.vsdiat.com

2. https://github.com/stevehoover/RISC-V_MYTH_Workshop

3. http://makerchip.com/sandbox/

4. https://github.com/kunalg123/riscv_workshop_collaterals

5. Alwin Shahju, colleague IIIT Bangalore

6. Lasya, colleague IIIT Bangalore

7. Bhargava DV colleague IIIT Bangalore

8. Pruthvi Parate colleague IIIT Bangalore



































 











 



 





















 









