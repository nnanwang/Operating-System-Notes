# CPU Scheduling

- **One processor -> one process running at a time** (Often running process doesn't need CPU *e.g., I/O requests*)
- **Multiprogramming goal: avoid CPU idle times -> some process is using the CPU all the time**
<img width="813" alt="Pasted Graphic 1" src="https://user-images.githubusercontent.com/74788199/224523734-03628289-9f0f-4165-b89d-7782ebb3807c.png">

### When Does the Scheduler Get Invoked?
1. When there’s a timer interrupt (running process has exceeded its time share)
2. When running process terminates
3. When running process issues an I/O request (block)

## CPU–I/O Burst Cycle
Programs are I/O bound more often than they are CPU bound<br>
![image](https://user-images.githubusercontent.com/74788199/225171795-627d30db-3e26-4b30-831f-27ddb4f5bcd1.png)
- **CPU-Bound** <br> - Highly dependent on the CPU <br> - Most times, the processor is the only component being used for excution <br> - Tend to have few and long CPU burst <br> ![image](https://user-images.githubusercontent.com/74788199/225171987-f239b223-d231-48a6-b6d8-857356e262e2.png) 
- **I/O-Bound** <br> - dependent on the input-output system and its resources *(e,g., disk drives and peroheral devices)* <br> - I/O bound operations are characterized by many and fewer CPU bursts <br>![image](https://user-images.githubusercontent.com/74788199/225188565-ccb7eb0e-2cee-4f91-831a-be6982b4f578.png)

|               | Advantages |  Disadvantages | 
| ------------- | ----------- |  ----------- |
| **CPU-Bust**      | The use of CUP results in **faster processing** of task or programs       | 1. **waste of recourcesthe** - use of the processing unit alone results in other system componnents being idle <br> 2. **Incresing CPU power**      |
| **I/O-Bust**      | Due to the short CPU bursts, they're assigned higher priority during scheduling to ensure system resources better used        | 1. **Slower than CPU-bound programs**<br> 2. Due to the use of input-output system, **the time spent warting for data to be read or written can be substantial.**         |

## Scheduling Metrics
How to measure effectiveness of Scheduling Policies?
- **CPU Utilization** - percentage of time that CPU is doing useful work *(good = high)*
- **Throughput** - Number of processes that complete execution per time unit *(good = high)* <br> Throughput = **n** *(processes completed)* **/ time unit**
- **Turnaround Time** - Amount of time to execute a particular process, include time in ready and waiting queues. *(good = low)* <br>  **Turnaround time = Burst time + Waiting time** or **Turnaround time = Completion time – Arrival time**
- **Waiting time** - Average time process spends in Ready Queue *(good = low)*
- **Response Time** - Average time before process produce first response after request *(good = low)*

### Two Types of Scheduling
- **Non-Preemptive:** processes only give up CPU voluntarily (2,3 above)
- **Preemptive:** processes also may be preempted by timer interrupt (1,2,3 above)

## Scheduling Policies
### 1. FCFS *(first come first served)* - Non-preemptive<br>
<img width="550" alt="image" src="https://user-images.githubusercontent.com/74788199/218562669-b3096784-f53b-4af5-87ba-fef65b317384.png">

| **Advantages** |  **Disadvantages** | 
| -------------- |  ----------------- |
| - Easy to implement (ready queue = scheduling queue) <br> - No starvation |  Convoy Effect: Order of arrival determines performance |

### 2. SJF (shortest job first) 
- **Non-preemptive** <br> <img width="550" alt="image" src="https://user-images.githubusercontent.com/74788199/225339815-b054eb6c-aebd-4354-8ff7-3042893d3c98.png"> <br> <img width="550" alt="image" src="https://user-images.githubusercontent.com/74788199/225343212-7c9f1e4b-bac2-4174-a74d-74ee0ce6322c.png"> 

- **Preemptive** <br> <img width="550" alt="image" src="https://user-images.githubusercontent.com/74788199/225341540-7dc77efc-d948-4ad8-84b7-e83cb9c11c94.png">

**Summary**
- Issue: Predicting how much is next CPU burst
- Exponential Averaging
- Uses “history” of previous CPU bursts
- Predict length of next CPU burst <br> <img width="550" alt="image" src="https://user-images.githubusercontent.com/74788199/218564774-d9b13ecd-626a-49b8-9734-d4697de10dee.png"> <br> <img width="550" alt="image" src="https://user-images.githubusercontent.com/74788199/218564823-3581b757-15f4-4049-aff6-379ed979492f.png">

| **Advantages** |  **Disadvantages** | 
| -------------- |  ----------------- |
| Approximates optimal schedule for: <br> - Average wait time <br> - Average turnaround time |  Starves processes with expected long CPU bursts |

### 3. Priority Scheduling 
- **Non-preemptive** <br> - CPU Allocated to Process With Highest Priority <br> - Whenever running process blocks or terminates
- **Preemptive** <br> - CPU Allocated to Process With Highest Priority <br> - Whenever new process arrives or running process blocks or terminates
<img width="550" alt="image" src="https://user-images.githubusercontent.com/74788199/225350258-201d54b4-fe17-476c-aafe-6811e9abbb37.png">

| **Advantages** |  **Disadvantages** | 
| -------------- |  ----------------- |
| Reflects relative importance of processes *(e.g.: kernel > user)* |  - How is priority determined? <br> - Turnaround, wait times, process burst length ignored <br>- Starvation of low-priority processes *(Can counter with “aging” (process gets increasing priority the more it waits))* |

### 4. Round-Robin - Preemtive
- Each process gets small unit of CPU time (time quantum). 
- Preemptive: Process switch based on timer interrupts
- Fairness
<img width="550" alt="image" src="https://user-images.githubusercontent.com/74788199/218567633-cbc69776-0fc7-424a-87f2-e1b32ee628c8.png">

| **Advantages** |  **Disadvantages** | 
| -------------- |  ----------------- |
| - Fairness <br> - Response time <br> - Simple |  - Turnaround time <br> - Cost of context switches (Must choose quantum carefully) |

<img width="550" alt="image" src="https://user-images.githubusercontent.com/74788199/218568169-d2638782-6876-40be-bd1b-5f3574185f43.png">

### 5. Multilevel Queues, Lottery 
- Ready queue is partitioned into separate queues, each with own scheduling algorithm
- Requires Interqueue Scheduling Too (Scheduling of Queues)
<img width="712" alt="image" src="https://user-images.githubusercontent.com/74788199/218569455-4ba2b43c-7cb5-4eff-afe7-a49455b42a17.png">

**MFQ** *(Multilevel Feedback Queue)* **Scheduler Must Have Following Parameters:**
1. Number of queues
2. Scheduling algorithms for each queue
3. Scheduling algorithm between queues (or CPU time-slices)
4. Upgrade process (e.g.: Aging)
5. Downgrade process
6. Initial queue determination process

**Observe**
1. Average turnaround time: 3100 / 6 = 516.7
2. Shorter jobs tend to have shorter turnaround times

## CPU Scheduling Summary

<img width="773" alt="image" src="https://user-images.githubusercontent.com/74788199/218570960-84ad686f-91bf-44ba-a832-bf5cb4e76e12.png">

## Real-Time Scheduling
### 1. Hard Real-Time *(Must complete by some deadline)*
can be integrated into MFQ’s
- Determine “feasible” processes (deadline – now 3 burst)
- Re-determine at every context switch
- Choose process with min value of [deadline – (now + burst)]
![image](https://user-images.githubusercontent.com/74788199/225477175-465479ea-3891-40fd-bf8f-582162d966b5.png)

### 2. Soft Real-Time *(Should complete by some deadline)*
requires dedicated scheduler
**Can be integrated into priority-based scheduler** *(e.g.: MFQ’s)*
- should not be demoted
- requires strict time-slices



