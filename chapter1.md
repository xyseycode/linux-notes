Layers of abstraction in a Linux system (organization of the system)
User processes
    gui, webserver, shell 
Kernel Processes
    process management, memory management, device drivers
Hardware
    cpu, main memory (ram), hard disk, network ports

Kernel - the core of the system, it is the software that resides in main memory and tells the cpu what to do next. It's the glue between the processes and the hardware.

User space - it is the sub-space in memory that the user can access, all the user processes are here (user mode)
Kernel space - the space in memory that the kernel has access to, all the processess that have kernel mode are here. All processes in kernel mode have unrestricted control over the cpu and memory, so be responsible with the priveleges. 

State - is a particular collection of bits that states the state of process, memory...
eg. 1001, 0100... inn layman's term "the process is waitint for an input"

Four general system areas that the kernel manages
    Processes
    Memory
    Device Drivers
    System calls and support

Process management - is the term for starting, pausing, resuming, scheduling and terminating processes.
    Context Switching - when a process gives up control of the cpu to another process in a time slice(time for a process to control the cpu). The kernel manages context switching.
    EG: Suppose a web browser and a slide application are open, it's like the two process are simultaneusly running but that's not the case, they are using the cpu with the time slice they are given. If the CPU has only one core if it has 2 then the two process can have each of the core.

    Steps in the process manangement in a single core cpu
    1. The cpu will interupt the process and hands back the control to the kernel
    2. The kernel will record the state of the memory and the cpu, this is essential for the interrupted process to resume.
    3. The kernel will caught up with information that had gathered during the recent time slice so it will know what will it do.
    4. The kernel will choose one of the process that has been lined up.
    5. Kernel will prepare the memory and the cpu for the process to be run.
    6. It will tell the cpu of the time slice for the process.
    7. Kernel will turn the cpu in user mode to run the process.

    The kernel runs everytime the time slice of a process is finished to prepare the cpu for the context switch.

Memory Management - during context swithch the kernel must manage the memory of the system, these conditions must hold
    - the kernel must have a space in memory the user mode process can't access
    - each user process needs it's own section in memory
    - a process can't access a private memory of another process
    - user processes can share memory
    - some memory of processes are read only
    - the system can use more than the physical number of memory, it can use the disk as auxillary
    MMU - memory management unit... it helps the kernel in management available for modern cpus.
        it makes the process imagine that it has the whole memory of the system.

Device drivers and management - device drivers are only accesible through kernel mode to prevent user processes having access to them. EG: it's ridiculous if a user process want's to turn off the computer it might crash it right?
    Device drivers have traditionaly been part of the kernel to be uniform.
    The kernel acts as the interface between processes and hardware, it's the kernel's job to operate the hardware.

System calls and support - are a sample of kernel features that user processes can use when they have task/s that they alone can't do well or can't do. EG: Opening, reading, and writing of  files involves system calls

Two system calls to know
    fork() - when the process calls fork(), the kernel will create a nearly identical copy of the process
    exec() - when the process calls exec(program), the kernel loads and starts program replacing the current process.

    nearly all the processes in user space starts from fork(), and most the time you need to run exec() to start a new program instead of creating a copy.
    Example of this is when you run the command ls in a shell...
    first the program that runs in the terminal will fork() the shell to make a copy of it, now in the newly created copy of the shell, it will run exec(ls) to show the list of files and directories on the current directory

User space - the space in memory that the user processes have access to.
    There 3 levels in user space.. the lower the level the closer the process is to the kernel, the higher the closer to the user.

Users: an entity that can run processes and own files.
    the kernel does not manage usernames but user ids

    root - or superuser the most powerful user in the system. and even though it is powerful it still run in the user mode not in the kernel mode.

  