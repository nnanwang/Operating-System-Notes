# Review for Exam 1

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
a process allows the operating system to hide the underlying complexity of the CPU and memory hardware and present a simpler 
and more organized view to the programmer. This abstraction makes it easier for developers to write software and for users to
run multiple programs simultaneously without having to worry about the intricacies of the hardware.

