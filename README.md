# In this repo I'm going to Include source code for creating threads and processes.

## Process 
A process is program in its execution state.
Concept of Process has two facets.

A Process is:
A Unit of resource ownership:

1. A virtual address space for the process image
2. Control of some resources (files, I/O devices...)


A Unit of execution:

1. process is an execution path through one or
    more programs 
    2. may be interleaved with other processes
    execution state (Ready, Running, Blocked...) and dispatching
    priority
## Threads
A light weight process which sharres common memory when created. 
THreads are sharing memory.
Certain threads will modifies same variables.

## Race Condition
For checking the race condition we created three threads and also created a function which increments itself everrytime it is called by a thread. Thus our mail functions increases and it gives us the desired value as lng as we provided the desired value. But when we created a looop inside the mail funciton and mad the value too high like I incremented a Millions time then it is not providing the desired output. Thus we came to the race condition. Multicore processor face this problem.
1. Read the value in mails
2. Increament the value 
3. Writing back to the memory 
This works fine when we are working with a single thread but when we intriduce multiple thread then it will gives us a garbage value which is not the desired output.

| Read File | #1    | #2    |
| :---:   | :---: | :---: |
| Increament | 301   | 283   |
| :---:   | :---: | :---: |
| Write file | #1    | #2    |
| :---:   | :---: | :---: |

This race condition ocuured for large value of loop iterator not for a small number because for small number first threads creates and execute the function body in less time and in that time second thread is created but for large value it takes more time second thread is created and it also calls the function which creates ambiguity. And we get wrong answers.

## solving the Race Problem with Mutex
Using a mutex we will solve 
1. This we will introduce Pthread_mutex 
2. Use pthread_mutex-Lock 
3. Then pthread_mutex_unlock
4. Initialise this in the main
5. Now run te program again 
6. You will get the right answer 
locking and unlocking of mutex is protecting like it is protecting the block of code wihtin in a bracket to be executed by another thread. If in above example thread1 is executing the code in function , while incrementing the value thread2 and thread3 cannot execute the same line. 

## How To Create threads In LOOPS
===================================
1. For i  = 0 created first thread Then we are also joining it
2. We are going to get only on thread  executing at a time
3. If we are doing both create and join in the same for loop then only one thread will execute and remaining will wait n watch.
4. We don't have to do such bu******
5. So to avoid this create another loop for join and make it seprate loop for create_function.
6. THings will start getting executed parallel 
7. All threads will be create and same time they will finish their execution

## How to Get A return Value from a function
1. If your function has a void return type no return value
2. pthread_join will take a refrence to pointer 
3. Void pointers are wild cards they canbe anything 
4. We cannot return a simple variable from the function because after execution stack frame of that function will be deallocated all variables will be de allocated. So for that we have to allocate chunk of memory Dynamically. 
5. In this we can access the value of function
