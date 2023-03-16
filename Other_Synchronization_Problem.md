# Other Synchronization Problems

**Synchronization Problems and Solutions:** <br>
![image](https://user-images.githubusercontent.com/74788199/225732397-d70df1af-e3b8-4f10-b55f-82e9f9edf6b6.png)

## 1. Bounded-Buffer Problem
Share buffer between producer thread and consumer thread
- **buffer** - circular queue
- **in** - points to next spot to insert into buffer
- **out** - points to next spot to remove from buffer

![image](https://user-images.githubusercontent.com/74788199/225732859-67c1c902-c06a-426e-b6e2-5b7c55e110c5.png)

### Synchronization Issues:
#### 1. shared variables:
- **buffer[N]:** shared by all
- **in** - shared by all producers
- **out** - shared by all consumers

#### 2. Full buffer:
ensure that producer doesn't try to insert into *(instead wait until not full)*

#### 3. Empty buffer:
ensure that consumer doesn't try to consume from *(instead wait until not empty)*

#### Pseudocode Solution (Buffer Size = N)
```
Semaphore mutex = new Semaphore (1);          // Binary
Semaphore empty = new Semaphore (N);          // Counting,  empty (cnt = # empty slots left)
Semaphore full = new Semaphore (0)            // “Reverse” Counting,  full (cnt = # full slots left)
```
![image](https://user-images.githubusercontent.com/74788199/225740241-c398f4a5-31cc-4aed-88b5-35f9cd54958f.png)

## Game of Orders
### The sequence of down and up operations:
- **Producer:** down(empty), down(mutex), up(mutex), up(full)
- **Consumer:** down(full), down(mutex), up(mutex), up(empty)

### Is order of *down* important? 
**Yes! Can cause deadlock!
```
Producer(item) {
    down(mutex);        // Block the others, including consumer
    down(empty);        // Full buffer. Block. Could wait forever!
    // Add to buffers up(mutex); up(full);
    up(mutex);
    up(full);
}
```

### Is order of *up* important? 
**No, except that it might affect scheduling efficiency
```
Producer(item) {
    down(empty);
    down(mutex);
    // Add to buffers 
    up(full);         // only one producer increments full at a time
    up(mutex);
}
```
### Bounded-Buffer in Java
![image](https://user-images.githubusercontent.com/74788199/225743743-20b22d3d-5a69-4b79-9d6b-074c42bc3261.png)

### Spin lock
Avoids inconsistencies but wastes CPU resources (unnecessary busy waiting)
```
public void insert (Object item) {
    mutex.acquire()           // Acquire lock for initial busy-wait check 
    while (count == SIZE) {
        mutex.release ();     // Drop the lock to allow other threads (like consumer) to run
        mutex.acquire();      // Re-acquire the lock for the next call to count==SIZE 
    }
    ...; 
}
```
**Problem:** if consumers are blocked for a long time on processing their current tasks and the queue is full, producers are always busy-waiting

```
public Object remove () {
    Object item;
    mutex.acquire();        // Acquire lock for initial busy-wait check 
    while (count == 0) {
        mutex.release();    // Drop the lock to allow other threads (like producer) to run
        mutex.acquire();    // Re-acquire the lock for the next call to count==0 
    }
    ...; 
}
```
**Problem:** if the queue is empty and producer threads have nothing to add for a long time, consumer threads are always busy-waiting unnecessarily

## 2. Readers-Writers Problem
You have a buffer of updatable data *(i.e.: not just insert & removes)* <br>
**2 Kinds Threads:** Readers & Writers
**Synchronization rules:** <br> Can allow access of: any number of readers at a time, or exactly one writer

#### An example: A Database
- **Database Reads = Queries**
- **Database Writes = Updates**<br><br>
if an update is taking place:<br> 1. cannot allow reads <br>2. cannot allow other writes

### Solution 1: A Readers-Favored Solution 
***Solving with Semaphores***
- binary semaphore (```rwlock```) + count of readers (*rcount*)
- 1st reader accuires ```rwlock``` (*rcount* = 1)
- last reader release ```rwlock``` (*rcount* = 0)
- need additional binary semaphore (**mutex**) tp ensure exclusive access to *rcount* 

```
integer rcount = 0;                       // # of readers reading
Semaphore mutex = new Semaphore (1);      // binary, for rcount
Semaphore rwlock = new Semaphore (1);     // binary, for DB
```
```
Reader Thread

while (true) { 
    mutex.acquire();
        rcount++;
        if (rcount == 1)
            rwlock.acquire(); 
        mutex.release();
        
        <read database>
    
        mutex.acquire(); 
        rcount--;
        if (rcount == 0)
            rwlock.release(); 
        mutex.release();
}
```
```
Writer Thread

while (true) { 
    rwlock.acquire();
    
    <update database>
    
    rwlock.release(); 
}
```

















