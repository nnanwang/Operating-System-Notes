# Disk
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

### OS can try to improve disk performance
- By Reducing Seeking and rotation delay
- Increase file block
- Co-locate “related” items in order to reduce seeking
- ”Scheduling” access to blocks to optimize
- By improving caching



