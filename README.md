VLSI Physical Design for ASICs
Objective
The objective of VLSI (Very Large Scale Integration) physical design for ASICs (Application-Specific Integrated Circuits) is to transform a logical design description (RTL - Register Transfer Level) into a physical layout that can be fabricated as an integrated circuit. This involves translating the high-level functional representation of the circuit into a physical implementation that meets design constraints, performance targets, and manufacturability requirements.

SKILL OUTCOMES
Architectural Design
RTL Design / Behavioral Modeling
Floorplanning
placement
clock Tree Synthesis
Routing
INSTALLATION
https://github.com/kunalg123/riscv_workshop_collaterals/blob/master/run.sh

Download the run.sh
Open terminal
cd Downloads
./run.sh
TABLE OF CONTENTS
DAY 1
Introduction to RISCV ISA and GNU Compiler Toolchain

Introduction to Basic Keywords

Introduction
From Apps to Hardware
Detail Description of Course Content
Labwork for RISCV Toolchain

C Program
RISCV GCC Compiler and Dissemble
Spike Simulation and Debug
Integer Number Representation

64-bit Unsigned Numbers
64-bit Signed Numbers
Labwork For Signed and Unsigned Numbers
DAY 2
Introduction to ABI and Basic Verification Flow

Application Binary Interface

Introduction to ABI
Memory Allocation for Double Words
Load, Add and Store Instructions
32-Registers and their ABI Names
Labwork using ABI Function Calls

Algorithm for C Program using ASM
Review ASM Function Calls
Simulate C Program using Function Call
Introduction to Basic Keywords
Introduction
ISA (Instruction Set Archhitecture)

ISA defines the interface between a computer's hardware and its software, specifically how the processor and its components interact with the software instructions that drive the execution of tasks.
It encompasses a set of instructions, addressing modes, data types, registers, memory organization, and the mechanisms for executing and managing instructions.
RISC-V (Reduced Instruction Set Computing - Five).

It is an open-source Instruction Set Architecture (ISA) that has gained significant attention and adoption in the world of computer architecture and semiconductor design.
RISC architectures simplify the instruction set by focusing on a smaller set of instructions, each of which can be executed in a single clock cycle. This approach usually leads to faster execution of individual instructions.
image
From Apps to Hardware
Apps: Application software, often referred to simply as "applications" or "apps," is a type of computer software that is designed to perform specific tasks or functions for end-users.

System software: System software refers to a category of computer software that acts as an intermediary between the hardware components of a computer system and the user-facing application software. It provides essential services, manages hardware resources, and enables the execution of application programs. System software plays a critical role in maintaining the overall functionality, security, and performance of a computer system.'

Operating System: The operating system is a fundamental piece of software that manages hardware resources and provides various services for both users and application programs. It controls tasks such as memory management, process scheduling, file system management, and user interface interaction. Examples of operating systems include Microsoft Windows, macOS, Linux, and Android.

Compiler: A compiler is a type of software tool that translates high-level programming code written by developers into assembly-level language.

Assembler: An assembler is a software tool that translates assembly language code into machine code or binary code that can be directly executed by a computer's processor.

RTL: RTL serves as an abstraction level in the design process that represents the behavior of a digital circuit in terms of registers and the operations that transfer data between them.

Hardware: Hardware refers to the physical components of a computer system or any electronic device. It encompasses all the tangible parts that make up a computing or electronic device and enable it to perform various tasks.

Detail Description of Course Content
Pseudo Instructions: Pseudo-instructions are used to simplify programming, improve code readability, and reduce the number of explicit instructions a programmer needs to write. They are especially useful for common programming patterns that involve multiple instructions. Ex: li, mv.

Base Integer Instructions: The term "base integer instructions" refers to the fundamental set of instructions that form the foundation for performing basic arithmetic, logical, and data movement operations. Ex: add, sub, and, or, xor, sll.

Multiply Extension Intructions: The RISC-V architecture includes a set of multiply and multiply-accumulate (MAC) extension instructions that enhance the instruction set to perform efficient multiplication and multiplication-accumulate operations. Ex: mul, mulh, mulhu, mulhsu.

Single and Double Precision Floating Point Extension: The RISC-V architecture includes floating-point extensions that provide support for both single-precision (32-bit) and double-precision (64-bit) floating-point arithmetic operations. These extensions are often referred to as the "F" and "D" extensions, respectively. Floating-point arithmetic is essential for handling real numbers with fractional parts and for performing accurate calculations involving decimal values.

Application Binary Interface: ABI stands for "Application Binary Interface." It is a set of rules and conventions that govern how software components interact with each other at the binary level. The ABI defines various aspects of program execution, including how function calls are made, how parameters are passed and returned, how memory is allocated and managed, and more.

Memory Allocation and Stack Pointer

Memory allocation refers to the process of assigning and managing memory segments for various data structures, variables, and objects used by a program. It involves allocating memory space from the system's memory pool and releasing it when it is no longer needed to prevent memory leaks.
The stack pointer is a register used by a program to keep track of the current position of the program's execution on the call stack.
Labwork for RISCV Toolchain

C Program
We wrote a C program for calculating the sum from 1 to n using a text editor, leafpad.
![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/f1b66028-3d31-4f26-ae4f-1d48e21d577f)
#include<stdio.h>

int main(){
	int i, sum=0, n=111;
	for (i=1;i<=n; ++i) {
	sum +=i;
	}
	printf("Sum of numbers from 1 to %d is %d \n",n,sum);
	return 0;
}

running of spike commands

![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/ed2cbcd6-fe10-4a4e-b8a8-f2f851a1d99d)

running of signed and unsigned numbers
![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/4b6d7c4f-c309-4808-b61c-c0621c3e0a6f)
![image](https://github.com/ughdeiek/pes_asic_class/assets/142580251/419d8786-6524-4b00-a5d1-b8085f88e898)








