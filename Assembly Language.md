# Assembly Language

- Mem -> Reg: ```LOAD```
- Reg -> Mem: ```STORE```

## BL Algorithm

```
R3:= 0
R2:= SIZE_OF_TARGET
While R3 < R2 DO
  R1:= Disk [FIXED_DISK_ADD + R3]
  M FIXED_MEM_ADD + R3]:= R1
  R3:= R3 + 4
 GOTO FIXED_MEM_ADD
```

## Instruction
- **rect Addressing Mode:** -Move contents of address 21000 into R1 - ```LOAD R1, 21000```
-  
