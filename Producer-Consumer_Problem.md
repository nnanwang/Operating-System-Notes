# Producer-Consumer Problem
A Shared-Memory Solution to Bounded Buffer

## Bounded Buffer
- A Different Programming Mindset: Multiprogram Aware
- But Not an Infinite Loop Assuming Multiprogramming
<img width="761" alt="image" src="https://user-images.githubusercontent.com/74788199/217641358-50424dfc-1d5e-46be-a854-339de2e4c7f9.png">

- Multiprogramming Mindset Is More Difficult <br>
*e.g.: What if we context switch out of producer after count incremented but before
item added to buffer?*
<img width="619" alt="image" src="https://user-images.githubusercontent.com/74788199/217642138-e32b4ab6-60f7-4513-b9d9-c1d4f6173e12.png">

