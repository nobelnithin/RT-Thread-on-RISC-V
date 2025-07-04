# RT-Thread Kernel Introduction

The kernel is the core of an operating system and serves as its most fundamental and essential component. It is responsible for managing system threads, inter-thread communication, the system clock, interrupts, and memory.

The diagram below illustrates the RT-Thread kernel architecture, showing that the kernel sits above the hardware layer. The kernel section includes the kernel library and the real-time kernel implementation.

![image](https://github.com/user-attachments/assets/10bf3de2-84dd-4e44-8661-d5723fb3e10d)

## Thread Scheduling:  
The thread is the smallest scheduling unit in the RT-Thread operating system, which employs a preemptive multi-thread scheduling algorithm based on priority. In this system, only interrupt handlers, code that locks the scheduler, and code that disables interrupts are non-preemptible (meaning they cannot be interrupted). All other parts, including the thread scheduler itself, are preemptible.

The system supports up to 256 thread priorities, which can be configured to a maximum of 32 or 8. Priority 0 represent higher priority, while lowest priority reserved for the Idle thread. The system also support to create multithread with the same priority. These threads are scheduled using time slicing round robin algorith,ensuring each thread run for a designated time. Also the time take by the scheduler to locate the highest priority thread is constant. There is no limit on the number of threads, the actual number is only constrained by the specific of the hardware platform.

## Synchronization Between Threads
RT-Thread implements inter-thread synchronization using semaphores, mutexes and group events. Threads synchronize by acquiring and releasing the semaphores and mutexes. Mutex employes the priority inheritence mechanism to address the common priority inversion problem found in the real time systems. The thread sysnchronization mechanism allows the thread to wait for the semaphores and mutexes based on their priority.
Threads synchronize by sending and receiving events. The event group supports for both "OR-Triggered" and "AND-Triggered" multi scenarios, making them suitable for case where it need to wait for multiple events.

## Inter Thread Communication
RT-Thread supports communication mechanism such as mailboxes and message queues. Each message in the mailbox has fixed length of 4 bytes, where message queues can receive message of variable length and store them in their own memory space. Mailboxes are generally more efficient than queues. Sending operation can be done for both mailbox and queue safely by interrupt service routine(ISR). The communication mechanism allow thread to wait for the message based on the priority.

## Clock Management 
RT_Thread's Clock Managemt is based on the Clock tick, which is the smallest unit of time in RT_Thread operating system. RT-Thread provides two types of timer mechanism, first is one-short timer, which triggers a timer event only once after it starts and then automatically it will stops. Second one is periodic timer, which continuously triggers timer event until user manually stops the timer, allowing to it to run undefinitely. Additionally we can execute timeout fuction, in RT-Therad timer can the configured in either "HARD_TIMER" mode or "SOFT_TIMER" mode. Typically timers are used to execute callback function(i.e., timeout function) to fullfill the timing service requirement. User can choose appropriate type of timer based on the real-time rerquirements of timing operation.

## Memory Management 
In a computer system, variables and intermediate data will be stored in RAM and load in CPU when ever it is needed. In RT-Thread's memory management various memory allocation algorithm are provided to meet specific need of different aplication and system resource. These algorithm are boardly classified into two main categories: Heap memory management and memory pool management. Heap memory management is further divided into three: 1) Small memory management algorithm 2) slab management algorithm(large memory block) 3) memheap managemant algorithm(multiple memory heap)
