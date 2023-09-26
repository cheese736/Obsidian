# Processes and threads
A process is an executing program.
An operating ststem uses processes to separate the applications that are being executed. A thread is the basic unit to which an opreating system allocates processor time.
Each thread has ==scheduling piority== and maintains a set of structures the system uses to save the thread context when the thread'sexecution is paused. The thread context includes all the information the thread needs to seamlessly resume execution, including the thread's set of CPU registers and stack.
Multiple threads can run in the context of a process. All threads of a process share its virtual address space. A thread can execute any part of the program code, including parts 
