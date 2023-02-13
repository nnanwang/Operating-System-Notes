# Review for Exam 1

## Asembly
- Mem -> Reg: ```LOAD```
- Reg -> Mem: ```STORE```
## Interrupts
### Interrupts notify CPU through raising Interuppt Request flag (IR Flag)
### IR Flag Implementations
- 1 line
- Interrupt Vectors

### When does the IR Flag get checked?
- Within the fetch-decode-execute cycle by the control unit

### What happens once the interrrupt is recognized?
**interrupt handling**
- save processor "state"
- identify the interrupt device
- set PC to address to appropriate "device handler"
- device handler performs transfer of data from deceive controller registers to CPU
 
 ## OS Operations
 OS and users share the hardware and software resources of a computer system
 - Sharing system resources
 - Ensure an incorrect/malicious program does not cause other problem
 
 ## 2 Modes of Operation
 
 I/O instructions are privilliged, what assembly instructions need to change mode to kernel when executing?
```read``` and ```write```

What are the purposses of OS?

## Process
- Abstraction of the CPU aand main memory
- program in execution
How is a process an abstraction of the CPU?
A process allows the operating system to hide the underlying complexity of the CPU and memory hardware and present a simpler 
and more organized view to the programmer. This abstraction makes it easier for developers to write software and for users to
run multiple programs simultaneously without having to worry about the intricacies of the hardware.

CPU - time-sliced
Memory - space-sliced

- Multiple processes increase CPU utilization 

Processes are independent.
Threads can share memory, so we say thread is an abstraction only for CPU

### What's in a Process>
- Code section
- Data section -> global variables
- Stack (stack segment) -> local variables, function parameters
- Registers

### Process status
- New
- Running
- Waiting 
- Ready
- Terminated

### Process and Memory
1. program has access to all memory <br>
Memory is partitioned amongst processes
2. Memory is continuos

### Motivation for threads
1. Allocate Memory 2. Copy Text
3. Copy Data <br>
4. Copy Stack
5. Copy File Descriptors
6. Copy Registers
7. Copy PC, IR, Stack PTR Reg, Status Reg

### User Threads vs Kernel Threads
- kernel Threads




