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

## Deadlock Prevention
***Prevention = breaking one of the 4 conditions*** *(except for mutual exclusion)*

### Hold & Wait
**Defined:** Process holding a resource waiting to aquire others held by other process.

#### Deadlock Prevention
Use a lock to ensure if you get one, you get all the required resources

#### Challenge
Sometimes hard to know all the required resources

#### Disadvantage
- Lead to poor resource utilization, starvation is possible
- Dcrease concurrency since lockes acquired early rather when truly needed

### No Preemption
**Defiend:** Resources only released voluntariry.

#### Deadlock Prevention
If process holding resources requests another it can't get, must release all resources it holds.
- Released resources now added back to those process is waiting for
- Process only restarts when it can get old and requested resources

#### Implementation
e.g. using Java ```trylock()```

## Circular Wait
**Defined:** P1 *waits for...,* P2 *waits for ...,* Pn *waits for* P1

### Deadlock Prevention
Impose ordering on resource types
*(e.g.: R1 < R2 < ... < Rn)*
- process must request resources in increasing order
- deadlock prevented because deadlock requires: <br>![image](https://user-images.githubusercontent.com/74788199/234442511-f250d0bc-3afc-44c8-aac9-9d04851c44f0.png)

### Try before locking
#### Pattern
- Thread 1: 
  ```
  Top: lock1.lock(); 
  if false = lock2.trylock() {
      lock1.unlock(); 
      goto Top
  }
  ```
- Thread 2: 
  ```
  Top: lock2.lock(); 
  if false = lock1.trylock() {
      lock2.unlock(); 
      goto Top
  }
  ```
  
 #### Disadvantage
 Could create livelock - not deaadlock but no progress
 
 #### Approach is hard to implement

### Summary of Deadlock Prevention
| ***Precondition*** | ***Removal***|
| ------------------ | ------------ |
| **Mutual Exclusion** | can't move it |
| **Hold and Wait**| Request all resources at start. Proceed if granted (dp-lock) |
| **No Preemption** | If request denied, release all resources being held (```trylock()```)|
| **Circular Wait** | Order resources and request in order|

## Deadlock Avoidance

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
- Based on priority 
- Based on completion percentage
- Based on resources held
- Based on resources requested Interactive vs. Batch
### How do we recover?
- What state are we left with?
- Very messy. Often impractical




