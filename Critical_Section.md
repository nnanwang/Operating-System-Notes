# Criticle Section
Piece of code that only one thread can execute at any time

## Solutions to guarantee
- **Mutual exclusion:** no more than 1 process at a time
- **Progress:** cannot keep postponing scheduling process into its
critical section if no other is in its critical section
- **Bounded waiting:** once a process requests entering critical section, there
must be a bound on # of other processes allowed to
enter their critical section before granted

### Algorithm 1: Strict Alternation
Assumes that Thread A and B need it equally -> its not. 
Uses a shared turn var to track who's turn 

### Algorithm 2: "After You"

### Algorithm 3: Peterson’s Algorithm
- Combines ideas from algorithms 1 and 2.
- Threads take turns, Thread skips its turn if not interested and another thread is

<img width="763" alt="image" src="https://user-images.githubusercontent.com/74788199/222252512-3ecce804-3971-4b97-9fe5-85f2a93eb435.png">

## Hardware Solutions to Synchronization
### Test-and-Set (TS)
```
TS (i) =
    1. temporarily saves value of Mem[i]
    2. sets Mem[i] := TRUE
    3. returns original value of Mem[i]
```
**Can be used to implement “locking”**
```
shared bool lock = FALSE;
while (TRUE) {
    while ts (lock) skip;
    <critical section>
    lock := FALSE
    <non-critical section>
}
```
**Helps of TS**
- **limited** <br>
Easy to use for critical sections <br>
Not easy to use for other synchronization problems
- **wasteful busy-waiting:** <br>
thread waiting for lock must loop <br>
```while (ts (lock) == TRUE) skip;``` <br>
can avoid busy waiting but code is complex
- **can be really expensive on multi cores :** <bt>
memory access, adds bus traffic…


