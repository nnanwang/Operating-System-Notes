# Processes versus Threads
Thread = “Lightweight Process”

| Decription  | Threads     |  Processes  |
| ----------- | ----------- | ----------- |
|             | Cheaper     |  Expensive  |
| Steps       | 1. Initiate Stack 2. Copy Registers 3. Copy PC | 1. Allocate Memory 2. Copy Text 3. Copy Data 4. Copy Stack 5. Copy File Descriptors 6. Copy Registers 7. Copy PC, IR, Stack PTR Reg, Status Reg   |

## Threads
### Canceling
- Any thread can cancel any other thread it knows about
- Interruptee thread must be implemented to periodically check
its interrupt flag
```isinterrupted()```: Returns true or false <br>
```interrupted()```: Returns true or false & clears interrupt flag
