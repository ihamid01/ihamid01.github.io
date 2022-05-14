
## How a program is turned into a process



How do we go from lines of code written by programmers to fully functioning programs? How are programs turned into processes by the operating system? In this post, I will aim to provide an overview of how the operating system is involved in turning your c code into something your cpu can execute.



The first step of running a program is to load and store its memory. Programs are first stored in the hard disk drive. The hard disk drive is often referred to as secondary memory; it’s where the operating system, applications, and files are stored on your device. Program data, which consists of code and static data such as initialized variables, needs to be put into the address space for that process. The operating system reads that data from the disk and stores it in the main memory. The main memory is also known as RAM (Random Access Memory). Why do we need to store it in main memory? If we were to access data directly from the disk every time it was required, it would take forever to run even simple programs. Like I said before, all your computer data is on the disk. The more data that is present on the disk, the longer it takes to retrieve it. The CPU can’t get data directly from the disk. Old operating systems used to load all the memory needed for the program into main memory, but now in most systems memory is only added as needed. This is more efficient in terms of speed and memory usage, as space in ram is limited and most laptops/computers usually have around or over 100 processes running at a time. The loading of memory is done through paging, segmentation, or both. Paging and Segmentation are both memory management schemes in which data is broken up into blocks and transferred from secondary memory to main memory.  Space in ram 



Once the information is loaded and stored in main memory, it needs to be organized a little further. Certain information is stored on the program stack, such as the return addresses, local variables, and function parameters. Why is this done? The stack is used to maintain scope. When a function is called its arguments and variables are pushed on the stack. When a block of code is pushed off the stack, its variables are forgotten. This way functions can’t use variables defined in other functions. When a function leaves the stack, it pops the address of the function caller of the stack and continues running code starting from that address. The OS allocates and initializes some memory for the process, such as the argc and argv array. 



In addition to storing memory on the stack, the OS also stores information on the heap. Have you ever used malloc to allocate memory to a pointer? Or created a global variable in a program? These variables were stored on the heap. Have you ever compiled a program and gotten a segmentation fault? That’s often because you were trying to reach memory not allocated for your program. The heap memory isn’t bound by any scope, it can be used throughout the program. Data structures that consist of pointers are stored on the heap, such as hash tables, linked lists, trees, and more. Data stored on the heap is dynamic. It also needs to be specifically malloced and freed by the programmer. When we call malloc, the OS can grant more memory space to the heap if it’s required. 



At this point, all the memory is loaded into ram, the stack and heap are initialized. There are some other initializing procedures for the OS to do, like setting up standard input, standard output, and standard error.  After that, all that’s left for the OS to do is call the main function and start executing the program. 


