# Processes versus Threads
Thread = “Lightweight Process”

| Decription  | Threads     |  Processes  |
| ----------- | ----------- | ----------- |
|             | Cheaper     |  Expensive  |
| Steps       | 1. Initiate Stack 2. Copy Registers 3. Copy PC | 1. Allocate Memory 2. Copy Text 3. Copy Data 4. Copy Stack 5. Copy File Descriptors 6. Copy Registers 7. Copy PC, IR, Stack PTR Reg, Status Reg   |

## Threads
- ```run()```: Defines code run by thread
- ```start()```: Called by parent to make child thread runnable
- ```join()```: Called by parent to wait for child to finish
- ```isinterrupted()```: Called by child to see if interrupt flag set
- ```interrupt()```: Called by parent to set interrupt flag of child
- ```Thread.CurrentThread()```: Returns currently running thread
- ```yield() , sleep()``` : Called by child to release own CPU

### Processes/Threads Not Always Running
<img width="753" alt="image" src="https://user-images.githubusercontent.com/74788199/218559840-8f0ddccd-f540-4933-9a31-d881cf505ab4.png">

### Canceling
- Any thread can cancel any other thread it knows about
- Interruptee thread must be implemented to periodically check
its interrupt flag
```isinterrupted()```: Returns true or false <br>
```interrupted()```: Returns true or false & clears interrupt flag
