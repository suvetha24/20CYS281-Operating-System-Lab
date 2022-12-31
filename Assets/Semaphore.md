# 20CYS281 - Operating System Lab 
![](https://img.shields.io/badge/Batch-CYS-lightgreen) ![](https://img.shields.io/badge/UG-blue) ![](https://img.shields.io/badge/Subject-OS-blue)

## Semaphore 

Semaphore is a non-negative integer variable used to signal the threads. It used wait() and signal() operations are used for process synchronization. 
In simple words, it is a **Signalling mechanism.**

### Header file

```
#include <semaphore.h>
```

### Function 

```
sem_init(&acqrel, 0, 1);
sem_destroy(&acqrel);
```

```
sem_wait(&acqrel);
sem_post(&acqrel);
```

### Example 1 - Binary Semaphore 

```
/*
@Author: Ramaguru Radhakrishnan
@Date: 28 - Dec - 2022
@Description: Semaphore
*/

#include <pthread.h>
#include <stdlib.h>
#include <stdio.h> 
#include <semaphore.h>
#include <unistd.h>

// Semaphore lock 
sem_t acqrel;

// Counter is the shared resource variable accessed by all threads
int counter;

// printWelcomeMessage will be called when the Thread is created in the main function 
// which takes string as an argument
void *printWelcomeMessage(void *names) {

   // Semaphore wait message   
   sem_wait(&acqrel);
   
   char *name = (char *)names; 
   
   printf("\n[THREAD] Entering Critical Section %d", ++counter);
   
   for(int i=0; i<400000000;i++);
   printf("\n[THREAD] Hello, Welcome %s.", name);
   
   printf("\n[THREAD] Exiting Critical Section %d", counter);
   
   // Semaphore signal message
   sem_post(&acqrel);
   
}

int main () {

   // thread defintion
   pthread_t threads[3];
   
   // parameter to be passed to the called function - printWelcomeMessage
   char names[10][15] = {"Amritha","Praveen","Ramaguru"};
   
   // initializing the binary semaphore 
   if (sem_init(&acqrel, 0, 1) != 0)
    {
        printf("\n semaphore init failed\n");
        return 1;
    }
   
   int result;
   
   for(int i = 0; i < 3; i++ ) {
   
      printf("\n[MAIN] Creating thread, %d", i);
      
      // Creating the threading and thus calling the function with parameter passed to it
      result = pthread_create(&threads[i], NULL, printWelcomeMessage, (void *)names[i]);
      
      if (result) {
      
         printf("Error in creating thread, %d ", result);
         exit(-1);
      }
      
   }
   
   pthread_join(threads[0], NULL);
   pthread_join(threads[1], NULL);
   pthread_join(threads[2], NULL);
   
   // destroying the semaphore 
   sem_destroy(&acqrel);

}
```

#### Output

<p align="center">
    <img src="images/output/MT/Mutex.png" width="350">
</p>
