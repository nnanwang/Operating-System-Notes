# Processes versus Threads
Thread = “Lightweight Process”

| Decription  | Threads     |  Processes  |
| ----------- | ----------- | ----------- |
|             | Cheaper     |  Expensive  |
| Steps       | 1. Initiate Stack<br> 2. Copy Registers<br> 3. Copy PC | 1. Allocate Memory<br> 2. Copy Text<br> 3. Copy Data<br> 4. Copy Stack<br> 5. Copy File Descriptors<br> 6. Copy Registers<br> 7. Copy PC, IR, Stack PTR Reg, Status Reg   |

## Threads
- ```run()```: Defines code run by thread
- ```start()```: Called by parent to make child thread runnable
- ```join()```: Called by parent to wait for child to finish
- ```isinterrupted()```: Called by child to see if interrupt flag set
- ```interrupt()```: Called by parent to set interrupt flag of child
- ```Thread.CurrentThread()```: Returns currently running thread
- ```yield() , sleep()``` : Called by child to release own CPU

### Processes/Threads Not Always Running
<img width="750" alt="image" src="https://user-images.githubusercontent.com/74788199/218559840-8f0ddccd-f540-4933-9a31-d881cf505ab4.png">

### Canceling
- Any thread can cancel any other thread it knows about
- Interruptee thread must be implemented to periodically check
its interrupt flag

```isinterrupted()```: Returns true or false <br>
```interrupted()```: Returns true or false & clears interrupt flag
