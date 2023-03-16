# Process / Thread Synchronization
- Shared data access in a multi-process or -thread world leads to problems
- Data inconsistencies and undesirable process / thread behaviors.
- Synchronization is an umbrella concept of algorithms to solve these problem

## Terminology
### 1. Race Condition
**Outcome of thread execution depends on timing of threads** <br>
*e.g.: Outcome 1: 2 bottles of milk (timing shown) <br>
Outcome 2: 1 bottle of milk (e.g.: Person 2 looks in fridge at 3:25)*

![image](https://user-images.githubusercontent.com/74788199/225479521-eef28ca6-efa3-4139-aff9-140929e6e7c8.png)

### 2. Synchronization
**Use of atomic** *(i.e.: uninterruptible)* **operations to ensure correct cooperation amongst threads** <br>
*e.g.: Suppose **atomic operation** is:
1. Look in fridge 
2. Go to store
3. Return with milk <br>

**Never end up with too much or too little milk**

### 3. Mutual Exclusion
Ensuring that only one thread does a particular thing

### 4. Critical Section
Poece of code that only one thread can execute at any time

### 5. Lock
Construct that prevents someone from doing something

e.g.: 1. lock before entering critical section <br>
2. Uncock when leaving critical section

### 6. Startvation
Occurs when 1 or more threads never gets access to critical section

## Synchronization Summary
1. Have hardware provide better <br> primitives than atomic ```LOAD```, ```STORE```
2. Build higher-level programming abstraction on above hardware instructions
```
lock :: acquire()
// wait until lock is free and grab

lock :: release()
// unlock, waking up waiter if any
```
Both ```acquire``` and ```release``` must be **atomic** <br>
![image](https://user-images.githubusercontent.com/74788199/225489906-3bfd965c-d603-4371-8146-95600691178d.png)
- Simple code
- Same code for all threads
- Does not favor any thread

# The Critical Sections Problem
Ensure that only one thread executes its critical section at a time *(avoid race condition)*
- **Mutual exclusion** <br> ![image](https://user-images.githubusercontent.com/74788199/225498192-f30f6520-54d8-4a86-a7eb-b4e90d932661.png)
- **Progress:** No thread outside of its critical section should block other threads <br> ![image](https://user-images.githubusercontent.com/74788199/225498235-65a4f8f4-cf21-4f25-8abb-d1ef7da0fe8b.png)
- **Bounded waiting:** thread should not wait indefinitely to enter its C/S <br> ![image](https://user-images.githubusercontent.com/74788199/225498304-5a26fd03-bb75-449b-beb6-0846c656e5ac.png)
 
## 1. Software Solutions
### Algorithm 1: Strict Alternation
Each thread takes turns getting access to its CS <br>

![image](https://user-images.githubusercontent.com/74788199/225506423-41023618-3acb-43b1-9884-6250f068b733.png)

**Mutual Exclusion? Yes!** <br>
**Progress? NO!**<br>
**Bounded Wait? Yes!** 
<br>Consider the case where B wants to enter its critical section, A is not in its critical section, but B can't enter because ```turn == 0```<br>

![image](https://user-images.githubusercontent.com/74788199/225635248-1c6ecb6f-3e95-47e3-a296-a9faddcc05cd.png)

**Disadvantages:** <br>
- **Horribly wasteful** - Processes waiting to acquire locks spin on the CPU
- If Process 0 is faster than Process 1, then Process 0 will constantly get blocked by waiting for Process 1 to finish critical section
- Not a serious candidate since, it vialates Bounded waiting

### Algorithm 2: "After You"
Thread specifies interest in entering critical section. Can enter is other thread is not interested.<br>

![image](https://user-images.githubusercontent.com/74788199/225643182-7f56541d-5e98-4267-8e07-680b942fb02c.png)

**Mutual Exclusion? Yes!** <br>
**Progress? NO!** - Both threads could express interest with neither allowed entry into crotical section. <br>
**Bounded Wait? NO!** - Possible for threads to starve forever <br>

![image](https://user-images.githubusercontent.com/74788199/225644044-b1479ebe-a9c6-49d1-a698-98ddb7d1f1e0.png)

### Alogorithm 3: Peterson's Algorithm
Combines ideas **Strict Alternation** and **"After You"**. <br>
Threads take turns, but a thread skips its turn if it’s not interested and another thread is interested.

![image](https://user-images.githubusercontent.com/74788199/225649187-6331d9c2-5cce-46bb-9422-2076e6d39607.png)<br>
- thread A gets accessto C/S ```if(flag1 == FALSE) or (turn == 0)```
- thread B gets accessto C/S ```if(flag0 == FALSE) or (turn == 1)```

**Mutual Exclusion? Yes!** <br>
**Progress? Yes!**<br>
**Bounded Wait? Yes!** - if one thread waiting, need only wait until other thread sets value of turn

### Summary: Aproaches to Solve C/S
| Algorithm   | Idea        | Mutex?      | Progress?   | Bounded Wait? |
| ----------- | ----------- | ----------- | ----------- | ------------- |
| **Strict Alternation**    | Threads take turns entering C/S | :white_check_mark: | :x: | :white_check_mark:  |
| **"After You"**           | Threads enter C/S when no others want to | :white_check_mark: | :x: | :x:  |
| **Peterson’s Algorithm**  | Combines above 2. <br> Thread enters C/S when its turn, or thread whose turn it is, is not interested | :white_check_mark: | :white_check_mark: | :white_check_mark: |

## Better Way to Solving C/S
## 2. Hardware solutions
### 2.1. Disabling interrupts
Threads code works as follows:

![image](https://user-images.githubusercontent.com/74788199/225663734-fb8e5ada-3312-476c-8cd3-9a94aa11d495.png)

| **Advantages** | **Disadvantages**  |
| -------------  | -----------------  |
| **Easy to see that it works**    | **1. Overkill** <br>  a. Disables all interuppts *(e.g.: I/O)* <br>  b. Disallows concurrency with threads in non-criticle sections <br><br> **2. Doesn't work for multicore systems** <br> *Each CPU has own interrupts: threads on different CPU’s can access their critical sections at same time* |

### 2.2. Test-and-Set (TS) Addtional synchronization AL primitives
New AL instructions (Atomic)
```
TS (i) =
    1. temporarily saves value of Mem[i] 
    2. sets Mem[i] := TRUE
    3. returns original value of Mem[i]
```

Can be used to implement "locking" <br><br>
![image](https://user-images.githubusercontent.com/74788199/225666932-1197b3a5-6fd2-44d6-be83-b379a156b31d.png)









