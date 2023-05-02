# Virtual Memory
- Motivation: increase the degree of multiprogramming in a running system 
- Means:
  1. High memory utilization, flexible memory allocation <br> -> allow allocated memory to be noncontiguous (chunked), out of order
  2. swapping and vitual memory <br> -> allow some processes to have address space fynamically mapped to physical memory

## Swapping
ready or blocked processes have no physical memory allocation. Instead, address space mapped to disk. <br> <img width="500" alt="image" src="https://user-images.githubusercontent.com/74788199/235554256-01d87639-1b6a-4d7b-83a9-36a29ff29ac7.png">


### Achieves Higher Degree of Multiprogramming
not limited by available memory, but by available disk

#### +: Easy to implement
- modify context-switch routine to add swap-out and swap-in

#### -: Performance
1. Expensive: May need a lot of disk I/O
2. Time-variable: Depends on process size

## Virtual Memory
ready, blocked or running process have some (but not all) of their allotment of physical memory <br>
<img width="500" alt="image" src="https://user-images.githubusercontent.com/74788199/235554226-1c56c550-0964-45fa-bead-2a1aadaa13d7.png">

- exploits logical memory abstraction
- only part of the program needs to be in memory for execution
- logical address space can be much larger than physical address space
- Physical memory can be shared by many processes
- more efficient process creation
- Implementation options:
  1. Demand Paging
  2. Demand Segmentation

### Demand Paging
#### Idea:
- Paging: Units of allocation are pages (fixed size) 
- Demand: Bring a page into memory only when it’s needed
  - less I/O needed
  - less memory needed ® more users allowable
- When is a page needed?
  - A: When it is referenced (read or written)

#### Implementation:
Straightforward extension of paging
![image](https://user-images.githubusercontent.com/74788199/235571821-b9f201b5-1352-4d47-85fa-a45ba998a629.png)

1. Valid/Invalid bit
   - one per page table entry
   - 1 => in-memory, 0 => on disk
2. Modified Address Mapping Algorithm
   1. split logical address into page number (p) & offset (d)
   2. consult page table to find frame p (f)
   3. if page table entry for p is valid, go to (d), else
      1. trap to page-fault routine in OS to bring p into free frame & update page table
      2. restart instruction
   4. compute physical address (f, d)
   5. submit memory request with (f, d)

![image](https://user-images.githubusercontent.com/74788199/235572039-038cf5a0-e230-4fee-8ede-df56478c3434.png)
[link="https://learn.zybooks.com/zybook/BRANDEISCOSI131APitoSalasSpring2023/chapter/10/section/2?content_resource_id=79808414"]

### Page Faults
#### Page Fault Rate: 0 <= p <= 1
- p = 0 => no page fault
- p = 1 => every reference is a fault

#### Effective Access Time (EAT)
EAT = (1 - p) * memory access time + p * (page fault overhead + swap page out + swap page in + restart overhead)
<br> ![image](https://user-images.githubusercontent.com/74788199/235572514-5e3697f0-546c-4250-a6e1-e928247498fe.png)

### Page Replacement
- When no free frames available during page fault
- Must evict a page
#### Page replacement Algorithm
- if page replacement not done well, swapped out page may need to be swapped in soon after
- **Goal:** minimize number of page faults

#### Policy 1: Fist-In-First-Out (FIFO)
- Idea: Replace the page that's been in memory the longest 
- Implementation: update page-timestamp for every page fault
![image](https://user-images.githubusercontent.com/74788199/235685666-50b337e6-2f89-4751-a8e8-ea7d71e677b4.png)

**+:** easy to implement, understand
**-:** ignores page usage, Belay's Anomaly: more frames => lower hit radio

#### Policy 2: Optimal
- Idea: replace page that won't be used for the longest time
- Implementation: consult psychic to determin future page references
![image](https://user-images.githubusercontent.com/74788199/235689143-b7f55beb-181d-4ed9-925c-ea78f7f41678.png)

**+:** 
- achives optimal hit radio
- basic for performance comparisons with other policies
- basic for approximation policies (LRU, LFU)
**-:** not implementable

#### Policy 3: Least Recently Used (LRU)
- Idea: replace page with oldest page-timestamp
- Implematation: page-timestamp for every page in memory, update page-timestamp every time address references page
![image](https://user-images.githubusercontent.com/74788199/235691334-fcd19a26-ff75-432e-a801-deb57f80800b.png)

**+:** 
- assumes locality to predict future page accesses
- basic for approximation policies
**-:** overhead: system call (time) + write for each address reference

#### Policy 4: Approximations of LRU
1. **4a. Reference Bits**
   - add "reference bit" column to page table
   - intitially, all bits set to 0
   - reference to page p sets p's reference bit to 1
   - when all bits are 1, reset all to 0
   - when replacing, choose any page with reference bit = 0
   
![image](https://user-images.githubusercontent.com/74788199/235693714-f3abee40-41f5-4379-a80a-448d06cc51d8.png)

2. **4b. Refrence Bitstrings**
   - add n-bit column to page table
   - initially, all bits strings = 00...0
   - refrence to page p sets rightmost bit of page p's bit string to 1
     - e.g.: 01010010 -> 01010011
   - after fixed amount of time, shift all bit strings to the left
     - e.g.: 01010011 -> 10100110
     - efficient: most assembly langs have "shift left", "shift right" instructions for registers
   - Replacement: choose page with longest suffix of 0's

![image](https://user-images.githubusercontent.com/74788199/235697198-15e78771-e633-48dd-8f9e-8fbbc3e075ac.png)
<br>
![image](https://user-images.githubusercontent.com/74788199/235699244-919417d1-bddb-406c-88cc-fe31af4a8fd8.png)
Slow search

3. **4c. Second Chance**
   - combine reference bit w/FIFO
   - use FIFO, but pass on pages with reference bit = 1

3. **4d. Second Chance + "modifies bit**
   - some pages more costly to evict than others
     - pages that have changed since read, must be written
   - add "modified bit" column to page taable. Set to 1 when write to a page
   - favor eviction of pages with modified bit = 0

#### Policy 5: Least Frequetly Used (LFU)
- also tries to approximate optimal
- predicts that page that will not be accessed for longest time in future is that which has been accessed the fewest time in past
- requires maintaining counter for all pages in page table
![image](https://user-images.githubusercontent.com/74788199/235701810-027300bf-2005-4d56-8ef2-e06a8aa6ead6.png)

**+:** reasonable approximation of optimal in some cases
**-:**
- requires counter field in page table
- requires write of memory for every memory reference
- likely to evict pages just brought into memory
- less compatible with locality compared to LRU

## Summary
#### What if no free frames?
Page replacement

#### Goal
keep page fault fregquency low

#### Policies:
- FIFO
- Optimal (requires knowledge of the future)

#### Approximations of Optimal
- LRU (expensive)
  - Reference Bits
  - Reference Bitstring

- 2nd Chance (FIFO + Reference Bit)
- 2nd Chance + Modify Bit









