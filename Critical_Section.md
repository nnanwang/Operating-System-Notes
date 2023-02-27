# Criticle Section
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

