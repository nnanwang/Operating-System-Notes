# Deadlock
**occurs when 4 conditions hold:**
- Mutual exclusion
- Circular wait
- Hold and wait
- No pre-emption
***Prevention = breaking one of the conditions above*** *(except for mutual exclusion)*

## Hold & Wait
### Deadlock Prevention: Grab all at once 
**Hold & Wait:** Process holding a resource waiting to aquire others held by other process.

### Break Hold & Wait
- Use a lock to ensure if you get one, you get all the required resources
- Challenge: sometimes hard to know all the require

## No Preemption
### Deadlock Prevention: Try before locking
**Hold & Wait:** Resources only released voluntariry.

### Break No Preemption
- If process holding resources requests another it can't get, must release all resources it holds.
