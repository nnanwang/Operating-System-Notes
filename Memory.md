# Memory

## 3 Dedicated Registers:
- **MAR:** Memory Address Register
- **MDR:** Memory Data Register
- **CMD:** Command Register

*example of the register used*
```
STORE R1, <Addr>
  MDR:= R1
  MAR:= <Addr>
  cmd:= Write
  
LOAD R1, <Addr>
  MAR:= <Addr>
  CMD:= Read
  R1:= MDR
```
## Storage Devices and Memory
### Main Memory
Only large storage media that CPU can access directly (volatile) 
### Secondary Storage:
External memory that provides large, nonvolatile storage capacity

*examples:
magnetic disks, SD cards, compact flash cards, SSD, optical disks, magnetic tapes*

<img width="500" alt="image" src="https://user-images.githubusercontent.com/74788199/214680014-6d7b55b9-5b74-4c3b-b040-2e451be39f59.png">

### Devices
I/O Devices:
- Just I: Keyboard, mouse
- Just O: Monitor, printer
- Both: Disk

### "typical" numbers
- Sector = 512 byte
- seek 4-9 ms
- rotation avg =2 ms
- maxtransfer = 125MB/sec
- Random workload: *(e.g. access twitter account) *
- → Cost of seek and rotate dominates!
- SSD is faster than HDD on **random workload**
- SDD still more costly per capacity unit 60cent/GB vs 5 cent GB

## Interrupts
- Notify CPU
- Require hardware support
- Request flag (IR Flag)

### IR Flag Contents
- 00: No interrupts;
- 01: Device3 interrupted
- 10: Device1 interrupted
- 11: Device2 interrupted

### Responding to Interrrupts
<img width="736" alt="image" src="https://user-images.githubusercontent.com/74788199/214686588-0b054644-e077-4da0-be67-ea80f3a5d3f1.png">








