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
Both ```acquire``` and ```release``` must be **atomic**
![image](https://user-images.githubusercontent.com/74788199/225489906-3bfd965c-d603-4371-8146-95600691178d.png)
- Simple code
- Same code for all threads
- Does not favor any thread

## The Critical Sections Problem
Ensure that only one thread executes its critical section at a time *(avoid race condition)*
- **Mutual exclusion** <br> ![image](https://user-images.githubusercontent.com/74788199/225498192-f30f6520-54d8-4a86-a7eb-b4e90d932661.png)
- **Progress:** No thread outside of its critical section should block other threads <br> ![image](https://user-images.githubusercontent.com/74788199/225498235-65a4f8f4-cf21-4f25-8abb-d1ef7da0fe8b.png)
- **Bounded waiting:** Must be a bound on number of times other threads allowed to enter their critical sections after thread has made request to enter its critical section and before request granted <br> assume each thread executes at non-zero speed <br> ![image](https://user-images.githubusercontent.com/74788199/225498304-5a26fd03-bb75-449b-beb6-0846c656e5ac.png)
 
## Software Solutions
### Algorithm 1: Strict Alternation
Each thread takes turns getting access to its CS <br>
![image](https://user-images.githubusercontent.com/74788199/225506423-41023618-3acb-43b1-9884-6250f068b733.png)






