# Disk & File system
<img width="522" alt="image" src="https://user-images.githubusercontent.com/74788199/235800915-12bd9093-afdb-430f-aae3-d56fbc17ba8c.png">

## Secondary storage
- anything out of "primary memory"
- does not permit direct execution of instructions or data retrieval via machineload/store instructions 

### Characteristics:
- it’s large: 250-2000GB
- it’s cheap: $0.05/GB for hard drives
- it’s persistent: data survives power loss
- it’s slow: milliseconds to access

## Memory Hirarchy
<img height="300" alt="image" src="https://user-images.githubusercontent.com/74788199/234087496-041e1224-42f9-4405-9cdf-d5f8beecc96f.png"> <img height="300" alt="image" src="https://user-images.githubusercontent.com/74788199/234087586-694dfab9-a171-4ccc-9270-935d35d6d0a2.png">

## Disk and the OS
- Disks are messy, messy devices
- Job of OS is to hide this mess from higher-level software
- OS may provide different access to different levels
- Hardware support
![image](https://user-images.githubusercontent.com/74788199/235821509-8bf6c57e-b9be-44e8-8df5-7d24f63cf54c.png)


## Performance dependes on na number of steps
### Seek: moving the disk arm to the correct cylinder
- Depends on how fast disk arm can move
- Seek times aren't diminishing very quicly

### Rotation (latency): waiting for the sector to rotate under head
- Depends on rotation rate of disk
- Rates are incresing, but slowly

### Transfer: transfering data from surface into user
- from surface to disk controller
- from there sending it back to OS
- from there to the user
- depends on density of bytes on disk
- increasing, relatively quickly

### When the OS uses the disk
- it tries to minimize the cost of all of these steps
- oarticularly seeks and rotation

### OS can try to improve disk performance:

### By Reducing Seeking and rotation delay
- increase file block
- Co-locate "related" items in order to reduce seeking 
  - blocks of same file
  - data and metadata for a file
- "Scheduling" access to blocks to optimize

### By Improving caching
- keep data or metadata in memory
- prefetch block

### Seeks are very expensive
### FCFS (do nothing)
- reasonable when load is low
- long waiting time for long request queues

### SSTF (shortest seek time first)
- minimize arm movement (seek time), maximize request rate
- unfairly favors middle blocks

### SCAN (evevator algorithm)
- service requests in one direction unntil done, then reverse
- skews wait times non-uniformly

### C-SCAN 
- like scan, but only go in one direction
- uniform wait times

### Solid State Disks (SSD)
- more like RAM than spinning disk
- solid state drives are based on HAND flash memory

#### Reads
- Unit of read is a page, 4KB

#### Writes
- falsh media must be erased before it can be written to 
- unit of erase is a block, typically 640256 pages long
- unit of write is a page

#### Writing to an SSD is coplicated
- Random write to existing block:
  - read blck, erase block, write block, write back modified block
  - leads to hard-drive like perfromance
 
- sequential writes to erased blocks: fast

#### Higher level strategies can help hide the warts of an SSD

## Abstraction and Virtualization again
### physical address of data on disk
- depending on hardware there are layers of abstraction
- Blocks (have a certain fixed size, determined by the hardware)
- sometimes: platters
- somtimes: cylinders

### Blocks
- physical address of the data on the disk
- block address is (conceptual example) built up from <br>
![image](https://user-images.githubusercontent.com/74788199/235821733-0b99f47b-1bda-4375-a91f-bf50ec4580bb.png)
- think of the block address as the physical location of a block

### How do users access files?
- sequential access -> bytes read in order
- random access -> read/write element out of middle of array (gibe me bytes i-j)
- content-based access 

### Small Files design chanllenges
- finding the right file
- directories nneed to be able to store very large number of files
- file headers need to be efficient

### Large files design challenges
- writing a single large file can generate a huge amount of I/O
- creating, modifying and deleteing them create free space

## Disk Managemennt
#### Goal
- represent blocks on disk as a file
- create a useful abstraction

#### Common Data Structures
- each file has a header
- stores what disk blocks and sectors are associated with the file
- free space on disk
- blocks are numbered in cylinder major order
- adjacent numbered blocks can be accessed without seeks
- caching: of recently used blocks
- blocks in memory cana often be used














