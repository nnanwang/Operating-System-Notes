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



















