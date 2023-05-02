# Frame Allocation

## Fetch Policy 1: Demand Paging
pages are loaded on demand, not in advance
- It does not make sense to read an entrie program into memory at once
  - only a small portion of a program's code may be used!
  - for example, if you never use the "save as PDF" feature in Open Office...

## Fetch Plicy 2: Pre-paging
- Pre-paging - load pages before process runs
  - need a working set of pages to load on context switches
- Few systems use pure demand paging, but instaed, do pre-paging

#### Issue: One set of frames, multiple processes
<img width="500" alt="image" src="https://user-images.githubusercontent.com/74788199/235747116-3a1d7628-8566-48d9-a0c4-702aa29b9c66.png">

#### Goals:
1. Overall: Minimize page faults over all processes
2. Per process: Avoid any process "thrashing" (spends all time page faulting)

## 1. Local Allocation
**Idea:**
- assign a process some number of frames when it is created
- page fault requires ecicting a page that the process owns

**Issue: Thrashing**
- must provide minimum frame allocation to each process (as determined by instruction set)
- Otherwise, thrashing is inevitable

### Minimum Frame Allocation
#### Scenario
- Process P iterates over three arrays, x, y, and z, computing z(i) = x(i) + y(i)
- The three arrays are allocated to three different: array x is in page X, etc 
- The OS assigned only 2 frames to P
- Read x[0] notation is ← x[0], etc.

<img width="500" alt="image" src="https://user-images.githubusercontent.com/74788199/235767074-226ae90c-f06c-4c6b-bd9e-9d262a010d89.png">

### Some opinions
#### a. Equitable allocation: Each process gets [m/n] frames
- Problem: Suppose P1 needs 10 frames, P2 needs 190 frames, 60 are available
- Both get 30 frames and P1 has 20 frames that is doesn't need, and that P2 does need

#### b. Proportional allocation
- P1: (10 / 200) * 60 = 3 frames
- P2: (190 / 200) * 60 = 57 frames

#### c. Priority-based allocation
e.g.: Give P1 all 10 frames if it has a higher priority than P2

### Local allocation not used because...
- depends on knowing the set of "current" processes which changes dynamically
- assumes that a process' needs doesn't change over its lifetime
- assumes that frame availability doesn't change over a process' lifetime 

## 2. Global Allocation
**Idea:** all processes have access to all frames
**Global Replacement:** a page-fault in process P1 can replace a page owned by process P2 

### Thrashing still possible. A pathological example:
- P1 doesn't have enough frames, begins to thrash
- P1 takes frames from P2 in response. P2 begins to thrash
- chain reaction continues long enough, that scheduler notices CPU utilization is low due to thrashing
- scheduler response to low CPU utilization?
- increases degree of multiprogramming!!!
- more processes allowed in system => thrashing gets worse!

### Thrashing
Illustrating the Phenomenon<br>
<img width="437" alt="image" src="https://user-images.githubusercontent.com/74788199/235784199-3724c96b-ef62-4277-99b8-319c79dfdd0e.png">

#### Why does demand paging work?
A: Locality model
- process migrates from one locality to another
- localities may overlap

#### Why does thrashing occur?
∑ size of locality > memory size

### Working-Set Model
#### Working Set - A set of pages that a process is currently using
- If entire working set is in memory, no page faults!
- If insufficient space for working set, thrashing may occur.
  - Thrashing: process busy swapping pages in and out, i.e., processes spending more time paging than executing

#### Goal: keep most of working set in memory to minimize the number of page faults

#### The Working-Set Model
- based on locality - as process execures, it uses a different set of pages <br>
  <img width="663" alt="image" src="https://user-images.githubusercontent.com/74788199/235786009-21571a69-133a-46e3-b635-0a2b8cde3498.png">
 
- why does locality change? <br> e.g.: call of procedures

#### Goal: keep most of working set in memory to minimize the number of page faults

<img width="700" alt="image" src="https://user-images.githubusercontent.com/74788199/235783094-586eaaf4-09b9-432c-b537-4abf2ea37fd5.png">

### Working set Algorithm
Allocate enough frames to a process to fit the pages in its "current" locality
1. compute WSSi for each active process (1 <- i <= n)
2. 1. If ∑ WSSi  > available frames:
      - have thrashing. Must suspend 1+ process
   2. Else:
      - (re)allocate frames according to working-set sizes
      - if any frames left over, increase degree of multiprogramming

#### Issues:
1. what is the working-set window (Δ)?
   - Δ too small => does not encompass entire locality
   - Δ too large => encompasses several localities

2. Maintaining the working-set
   - accurate working-set too expensive to maintain
   - can approximate with reference bitstrings... 

###  Page-fault Frequently Scheme
Monitor page-fault rate of every active process. React accordingly <br>
<img width="564" alt="image" src="https://user-images.githubusercontent.com/74788199/235789668-ceaa74e2-6258-4ad5-8e49-994a7fac742f.png">

- if page fault rate > UB, allocate more frames
- if page fault rate < LB, dellocate frames
- may need to suspend process if cannot allocate more frames
- increase degree of multiprogramming if surplus

## Summary
### Frame Allocation
#### Goal: avoid thrashing
#### Global allocation：
1. working-set algorithm
   - used for allocation of frames per process
   - also used for deciding when to raise, lower degree of multiprogramming

2. Page fault frequency scheme
   - Also used for deciding when to raise, lower degree of multiprogramming

### Virtual Memory
- permits logical address space > number of acllocated frames
- permits higher degree of mutiprogramming than pure paging
- performance concern: keep page fault frequency low

### Page Replacement
- sessential tradeoff: low page fault frequency vs overhead to ensure
  - per memory access
  - periodic
  - per page fault
 
<img width="704" alt="image" src="https://user-images.githubusercontent.com/74788199/235798756-44eddba8-4f6a-4dba-b706-42773bb2e172.png">

## Processor & Core
<img width="450" alt="image" src="https://user-images.githubusercontent.com/74788199/235797959-900e824b-c5ea-4df9-95f5-0078227026d3.png"> <br>
<img width="450" alt="image" src="https://user-images.githubusercontent.com/74788199/235798040-17996544-f77e-4246-880a-ad6b964660ff.png"> <br>
<img width="450" alt="image" src="https://user-images.githubusercontent.com/74788199/235798128-3e7b354a-7d2b-40be-8bae-8563c5a0024b.png"> <br>
<img width="450" alt="image" src="https://user-images.githubusercontent.com/74788199/235798316-1774abb8-b011-49cd-abba-6d02c1474dda.png"> <br>
<img width="450" alt="image" src="https://user-images.githubusercontent.com/74788199/235798474-2ead9ef9-c44e-4255-999d-5ddca7c95088.png">

















