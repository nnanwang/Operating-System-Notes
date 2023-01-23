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
## Virtualization the CPU##
```diff
+ CPU - the Central Processing Unit
```






