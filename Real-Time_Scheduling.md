# Real-Time Scheduling

- **Hard Real-Time:** <br>Determine “feasible” processes (deadline – now >= burst) <br>Choose process with min value of [deadline – (now + burst)] <br>Re-determine at every context switch

- **Soft Real-Time**

# Synchronization
- Shared data access in a multi-process or -thread world leads to problems
- Data inconsistencies and undesirable process / thread behaviors.
- Synchronization is an umbrella concept of algorithms to solve these problem

## Terminology

### The Critical Sections Problem
Ensure that only one thread executes its critical section at a time (avoid race condition)


