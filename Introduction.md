# Introduction to OS

### **What is OS?** 
*OS is incharge of making sure the system operates correctly in an easy-to-use manner.*
- Responsible for making it easy to run programs
- Allowing programs to share memory
- Enabling programs to interact with devices, and other fun stuff like that

:computer: **Virtual Machine:** takes a **physical** resource *(the processer, memory, a disk)* and transforms it into a more general , prowerful, and easy-to-use **virtual** form itself. 

:closed_book: **Standard Library:** provides system calls to run programs, access memory and device, and other related actions.

:calendar: **Resource Manager:** manage the resources, doing so efficiently or fairly or indeed with many other possible goals in mind.

*Example:*
```
 #include <stdio.h>
 #include <stdlib.h>
 #include <sys/time.h>
 #include <assert.h>
 #include "common.h"

  int
  main(int argc, char *argv[])
  {
      if (argc != 2) {
          fprintf(stderr, "usage: cpu <string>\n"); 
          exit(1);
      }
      char *str = argv[1];
      while (1) {
          Spin(1);
          printf("%s\n", str);
      }
      return 0; 
  }
```
## Virtualizing the CPU
```Spin()``` 
- A function that repeatedly checks the time and returns once it has run for a second.
- Then it prints out the string that the user passed in on the command line, and repeats, forever.

## Memory: CPU Registers and caches
- General Purpurse Registers
- Status Registers
- Caches


### RAM: Random Acess Memory
- Volate RAW (dynamic RAW)
- Static RAW (SRAW): Read and written "automatically"
- ROW (read only memory)

```diff
- CPU - the Central Processing Unit
CPU = {ALU, CU}
```
ALU (Arithmetic Logical Unit) - Registers + Function Unit
<img width="700" alt="image" src="https://user-images.githubusercontent.com/74788199/214135964-7536c42c-3bc9-4eef-aef4-d91e8799ba8f.png">

- ## Assembly Language
 - Statements(instructions): CMP R1, R2
 - Low lever program language
 - All data used in computation in GPR's
 - Explicit movement of data
 
 ### System Calls
 - Mem - CPU operations (Assembly Language)
 - LOAD reg, mem-addr: Reg <- Mem
 - STORE reg, mem-addr: Reg -> Mem

## A process called ”loading”
- Reads the machine code file
- Determines where in memory to load it (so it can be executed) ¤ Copies the contents of the file to that location
- Loads the “PC” – Program Counter – with that address
- At which point the execution of that program kicks off (hihgly simplified:) 
*Fetch the instruction stored at location “PC” into the “Instruction Register”; 
Decode and execute the instruction in the IR; 
Increment PC by 1 word; 
Repeat.*

## System Calls
**Direct Addressing:**
- Syntax: ```READ Ri, Diskaddr```
- Meaning: 
**HALT

 ```LOAD```
- Syntax: ```LOAD Ri, @ Addr```
- Meaning: M[Addr] <- Ri







