# Deadlock
![image](https://user-images.githubusercontent.com/74788199/227751431-78e158c5-5ff4-49cd-b41e-6b32fd3a732c.png)

**occurs when 4 conditions hold:**
- Mutual exclusion
- Circular wait
- Hold and wait
- No pre-emption

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
