# 20CYS281 - Operating System Lab 
![](https://img.shields.io/badge/Batch-CYS-lightgreen) ![](https://img.shields.io/badge/UG-blue) ![](https://img.shields.io/badge/Subject-OS-blue)

## Mutex and Semaphore

### Mutex

Mutex is Mutual Exclusion Object. At any point of time, only one thread can work with the shared resources. In simple words, it is a **locking mechanism.**. 
A thread acquires a mutex when it is entering to access the shared/critical section of the program. The thread releases the mutex when it is exiting the 
shared/critical section of the program. A mutex can either be locked or unlocked which is modified only the process which requested or released the lock.

### Semaphore 

Semaphore is a non-negative integer variable used to signal the threads. It used wait() and signal() operations are used for process synchronization. In simple words, 
it is a **Signalling mechanism.**
