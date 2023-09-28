# Processes and threads
A process is an executing program.
An operating ststem uses processes to separate the applications that are being executed. A thread is the basic unit to which an opreating system allocates processor time.
Each thread has ==scheduling piority== and maintains a set of structures the system uses to save the thread context when the thread's execution is paused. The thread context includes all the information the thread needs to seamlessly resume execution, including the thread's set of CPU registers and stack.
Multiple threads can run in the context of a process. All threads of a process share its virtual address space. A thread can execute any part of the program code, including parts 



>When opening a new thread in a program, it incurs several resource costs. Thst costs may vary depending on the OS and programming language, but generally include:

1. Memory: Each thread requires memory for its stack, which is used for function call frames and local variables. The size of the stack can vary, but is typically a few MBs. The actual memory usage depends on the thread's stack size configuration.
2. CPU Time: Creating a new thread involves some CPU time for setting up the thread's data structures and context. This is generally a small overhead compared to the total CPU time a thread will use during its lifetime.
3. Thread Data Stuctures: The OS needs to allocate and maintain data structures for the new thread, such as a thread control block(TCB), which stores information about the thread's state and execution context.
4. Synchronization Overheads: if multiple threads access shared resources, you may need ==synchronization mechanisms==(e.g., mutexes or semaphores), which can introduce additional overhead in terms of PCU time and system calls.
5. Thread Management Overheads: The OS needs to manage the scheduling and context switching of threads. Switching between threads has some cost associated with it, including saving and restoring register values and other context-specific data.
6. Resouce Limits: Operating systems often have limits on the number of threads a process can create. Creating too many threads can lead to resource exhaustion and may result in errors or degraded performance.
7. Thread Lifetime: Threads consume resources for the duration of their lietime. While a thread is running, it uses CPU time and memory. When a thread terminates, its resources(including memory) are typically released.
8. Thred Creation Overhead: The process of creating a thread involves osme overhead, such as initializing the thread and allocating resources. This overhead is typically small compared to the total resource usage of the thread during its lifetime.