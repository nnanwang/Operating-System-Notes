# Lock
Lock::acquire is ```lock.acquire()```<br>
Lock::release is ```lock.release()```

- Lock is initially free
- Acquire to access shared data structure
- Always release after, only the lock holder should release. Don't let another method do it.
- Never access shared data without lock. 
- Always hold lock when calling ```wait```, ```signal```, ```braodcast```

Example - Bounded Buffer<br>
<img width="603" alt="image" src="https://user-images.githubusercontent.com/74788199/223221596-7053e98a-8c48-4f4c-87cd-0a0674d8bfdf.png">

## Condition Variables
- Always hold lock when calling ```wait```, ```signal```, ```braodcast```
- Condition variable does not remember previous state
- Wait atomically releases lock

### Use consistent structure
- Always use locks and condition variables
- Always acquire lock at beginning of procedure, release at end
- Always hold lock when using a condition variable
- Always wait in while loop

### call ```wait()``` 
<img width="547" alt="image" src="https://user-images.githubusercontent.com/74788199/223225619-0502b114-ef2d-40e2-836b-1c085821f0d2.png">
- When thread t calls ...
- t releases object lock
- t’s state = BLOCKED 
- t placed in wait set 
