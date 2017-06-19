---
title: CSAPP - 1
date: 2017-02-28 11:50:39
tags: 
  - Computer System
categories:
  - CSAPP
---
> There is a great well-known book, Computer Systems A programmer's perspective
I will post some notes after reading.

<!--more-->

### Computer systems
> Computer systems are a collection of hardware and software components that work together to run computer programs
> Everything in the system is a bunch of bits.The only thing that distinguishes different data objects is the context
in which we view them.

### Common phases in compiling system

* preprocessor
> Merge all referred files into source code

* Compile
> Translate source codes into assembly language

* Assembly
> Translate assembly language to machine language

* Link
> Merge all referred resource into result executable file. For example, some public system function

### Baic concepts of Hardware

* Bus
Running throughout the system is a collection of electrical conduits called buses that carry bytes of information back and
forth between the components. Buses are typicall designed to transfer size-fixed chunks of bytes known as words.The number
of bytes in a word is a fundamental system parameter that varies across systems.

* I/O devices

Input/output (I/O) devices are the system's connection to the external world. General input: Keyboard, Mouse. output: dsiplay
Each I/O device is connected to I/O bus by either a controller and adapter.
Controllers are chip sets in the device itself or on the system's main printed circuit board.
Adapter: a card that plugs into a slot on the motherboard. 

* Main memory
The main memory is a temporary storage device that holds a program and the data it manipulates while the processor is executing the program.
It consists of a collection of Dynamic Random Access Memory chips

* Processor
The central processing unit(CPU) is the engine that interprets instructions stored in the main memory.
**PC**: programming Counter points at some machinep-language instruction in the main memory.
The processor read instructions pointed by PC, execute the instruction, update **PC** to some next instruction.
*Load*: Copy a byte or word from Main Memory into register
*Store*: Copy a byte or word from register into main memory
*Upate*: Copy contents from two registers to ALU which puts result into a register
*I/O Read*: Copy a byte or a word from I/O device into register
*I/O write*: Copy a byte or a word from register to I/O device
*Jump*: Extract a word from instruction and copy that word into PC to update PC

### A common flow of execute helloworld
1. When we type hello on the prompt, the shell program reads each character into register, then stores it in the memory.
2. When we hit *enter* key on keyboard, the shell loads codes from disk to memory.There is a tech call DMA (Direct Memory Access)
3. Processor begins to execute instructions when the program is loaded into the memory. The processor copy instructions into register
4. Finally, copy *Hello World* to the display

### Operating System

> OS is a layer of software interposed between the application program and hardware

Purposes of OS:
1. To protect the hardware from misuse by runaway applications
2. To provide applications with simple and uniform mechanisms form manipulating hardware devices

### Process
> A process is the OS abstraction of a running program. Multiple process can concurrently on the same operating system, and each 
process appears to have exclusive use of hardware. By concurrently, we mean that the instructions of one process are interleaved with instructions of another process.The operating system performs this interleaving with a mechanism of context switch.
Operating system keeeps tracking of all the state information that the process needs inorder to run.This state, which is known as **Context**, includes information such as the current values of **PC**, the register file, and the contents of main memory.

### Thread
> Every thread is an execution unit of process in the context of a process, sharing the same code and global data.

### Virtual Memory
VM is an abstraction that provides each process with the illusion that it has exclusive use of the main memory.Each process has the
same uniform view of main memory, which is known as **Virtual Adress Space**


 
