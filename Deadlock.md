# Deadlock
![image](https://user-images.githubusercontent.com/74788199/227751431-78e158c5-5ff4-49cd-b41e-6b32fd3a732c.png)
### What?
Set of blocked processes/threads each holding a resource and waiting to acquire held by another process/thread in set.

## Occurs when 4 conditions hold:
1. **Mutual exclusion** - only 1 process can use a resource at a time
2. **Circular wait** - Exists a set of waiting processes, {P0, ..., Pn}
3. **Hold and wait** - Process holding 1+ resources is waiting to accquire others held by other process
4. **No pre-emption** - Resources only released by process voluntarily when finished using

## Resource Allocation Graph
**V = Set of vertices**<br>
- P = {P1, ..., Pn}: processes in system
- R = {R1, ..., Rn}: resource types in system

**E = Set of edges**
1. Request Edge: Pi -> Rj (process i requests resource j)
2. Assignment Edge: Ri -> Rj (recource j owned by process i)

<img width="671" alt="image" src="https://user-images.githubusercontent.com/74788199/234080328-b9d6145e-ccfa-483d-b807-5f00159a68cf.png">

***Prevention = breaking one of the conditions above*** *(except for mutual exclusion)*

## 3. Hold & Wait
### Deadlock Prevention: Grab all at once 
**Hold & Wait:** Process holding a resource waiting to aquire others held by other process.

### Break Hold & Wait
- Use a lock to ensure if you get one, you get all the required resources
- Challenge: sometimes hard to know all the require

## 4. No Preemption
### Deadlock Prevention: Try before locking
**No Preemption:** Resources only released voluntariry.

### Break No Preemption
- If process holding resources requests another it can't get, must release all resources it holds.

## Summary
| ***Precondition*** | ***Removal***|
| ------------------ | ------------ |
| **Mutual Exclusion** | can't move it |
| **Hold and Wait**| Request all resources at start. Proceed if granted (dp-lock) |
| **No Preemption** | If request denied, release all resources being held (trylock() |
| **Circular Wait** | |

## Deadlock Detection

**Cost: O (mn^2)**
- n = number of processes
- m = number of resources

## Deadlock Recovery
### Once Deadlock Discovered 
Processes need to be terminated
### Messy process:
- Kill all deadlocked processes
- Or, Kill 1 process at a time until deadlock cycle is eliminated
### In what order?
- Based on priority Based on completion percentage
- Based on resources held
- -Based on resources requested Interactive vs. Batch
### How do we recover?
- What state are we left with?
- Very messy. Often impractical




