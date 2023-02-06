# Process
## Unix Shell

```ps ax```

```ls –al```

```ps ax > myfile.out```
saves the list of all running processes to a file named "myfile.out"

```head myfile.out```  - displays the first 10 lines of the file "myfile.out"

```grep “eclipse” myfile.out``` performs a search for the string "eclipse" in the file "myfile.out"

```ps ax | grep eclipse``` list all of the processes running on the system and then filter the output to only show the lines that contain the string "eclipse"

```ps ax | more``` list all of the processes running on the system and then display the output one screenful at a time

*```more``` - allows to view the output one screenful at a time and navigate through the output by pressing the "space" bar to go to the next page, or the "q" key to exit.*

*```wc``` - word count*

## Memory Management
- **Defined:** large array of words, each with its own address
- **Directly:** accessible by CPU, devices
- **Volatile:** Loses Contents If Machine Power Cycles 

## File Management((Secondary Storage)

## I/O System Management(Devices)

## Processes versus Thread
Thread = “Lightweight Process” (no isolation)
- Abstraction only of CPU
- 1 process can have many threads (multithreading), all share the same memory

## What is a process?
*Processes not always **running***
<img width="625" alt="image" src="https://user-images.githubusercontent.com/74788199/216158076-31f7e243-c3d0-4328-9024-4a1c15274caf.png">

## OS handling of context switches
**PCB** = Process Control Block

*Suppose P0 is running and its time-slice end*
1. Update PCB0 <img width="180" alt="image" src="https://user-<img width="379" alt="image" src="https://user-images.githubusercontent.com/74788199/216159017-50727aeb-318d-44d4-bcf2-a900e063110f.png">

2. Add PCB0 to “ready queue”
3. Choose next process to run (Pi = f (Ready Queue, scheduling policy)\
4. Update CPU state with Pi’s context <img width="460" alt="image" src="https://user-images.githubusercontent.com/74788199/216158849-2206ac39-502d-4800-9b57-8c2cfa2209aa.png">

## Process Creation
Parent Process Create Child Process
*Like forming a genealogical tree*

```exit()```
Process executes last statement and asks OS to kill it
- Child may output data to waiting parent (WAIT system call)
- OS deallocates process’ resources

```kill()```
Parent terminates execution of child
- child exceeded allocated resources,
- task assigned to child is no longer required
- or parent exits (some OS do not allow child to continue if parent exits
- above can lead to cascading termination
- (Variety of KILL system calls)

```fork()``` create subprocess

## Message Passing
### Direct Communication
Processes Must “name” Each Other Explicitly
```
Send (P, message)
Receive (Q, message)
```

### Indirect Communication
Message directed anf receive from mailbox. 
Each mailbox has a unique ID
```
Send (A, message)
Receive (A, message)
```







