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




