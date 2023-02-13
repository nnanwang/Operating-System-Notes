# CPU Scheduling

The program counter (PC) is typically incremented by 4:<br>
Because it is the size of a typical instruction word in memory.

### When Does the Scheduler Get Invoked?
1. When there’s a timer interrupt (running process has exceeded its time share)
2. When running process terminates
3. When running process issues an I/O request (block)

### Two Types of Scheduling
- **Non-Preemptive:** processes only give up CPU voluntarily (2,3 above)
- **Preemptive:** processes also may be preempted by timer interrupt (1,2,3 above)

## Scheduling Policies
### 1. FCFS (first come first served) 
Non-preemptive<br>
<img width="632" alt="image" src="https://user-images.githubusercontent.com/74788199/218562494-fdda8185-8bee-4f7a-ab57-550d53301142.png"> <img width="752" alt="image" src="https://user-images.githubusercontent.com/74788199/218562669-b3096784-f53b-4af5-87ba-fef65b317384.png">
**Advantages**
- Easy to implement (ready queue = scheduling queue)
- No starvation

**Disadvantages**
- Convoy Effect: Order of arrival determines performance

### 2. SJF (shortest job first) 
a) Non-preemptive and b) Preemptive
<img width="719" alt="image" src="https://user-images.githubusercontent.com/74788199/218563313-a0357bf0-8a1a-43c9-a676-257f112a3688.png">
<img width="681" alt="image" src="https://user-images.githubusercontent.com/74788199/218563480-dfcc29a0-bcab-4148-8518-1827a169f717.png">
- Issue: <br>Predicting how much is next CPU burst
- Exponential Averaging
- Uses “history” of previous CPU bursts
- Predict length of next CPU burst <br> <img width="529" alt="image" src="https://user-images.githubusercontent.com/74788199/218564774-d9b13ecd-626a-49b8-9734-d4697de10dee.png"> <br> <img width="320" alt="image" src="https://user-images.githubusercontent.com/74788199/218564823-3581b757-15f4-4049-aff6-379ed979492f.png">

**Advantages** <br> Approximates optimal schedule for
- Average wait time
- Average turnaround time

**Disadvantages**
- Starves processes with expected long CPU bursts

### 3. Priority Scheduling 
a) Non-preemptive and b) Preemptive<br>
**Advantages:**
- Reflects relative importance of processes (e.g.: kernel > user)

**Disadvantages**
- How is priority determined?
- Turnaround, wait times, process burst length ignored
- Starvation of low-priority processes <br> Can counter with “aging” (process gets increasing priority the more it waits)

### 4. Round-Robin  
Each process gets small unit of CPU time (time quantum).  <br>
Preemptive: Process switch based on timer interrupts
<img width="737" alt="image" src="https://user-images.githubusercontent.com/74788199/218567633-cbc69776-0fc7-424a-87f2-e1b32ee628c8.png">

**Advantages**
- Fairness
- Response time
- Simple

**Disadvantages**
- Turnaround time
- Cost of context switches (Must choose quantum carefully)
<img width="721" alt="image" src="https://user-images.githubusercontent.com/74788199/218568169-d2638782-6876-40be-bd1b-5f3574185f43.png">

### 4. Multilevel Queues, Lottery 
Preemptive







