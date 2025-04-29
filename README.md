# cs2200-project-6-solved
**TO GET THIS SOLUTION VISIT:** [CS2200 Project 6 Solved](https://www.ankitcodinghub.com/product/cs2200-1-16/)


---

📩 **If you need this solution or have special requests:** **Email:** ankitcoding@gmail.com  
📱 **WhatsApp:** +1 419 877 7882  
📄 **Get a quote instantly using this form:** [Ask Homework Questions](https://www.ankitcodinghub.com/services/ask-homework-questions/)

*We deliver fast, professional, and affordable academic help.*

---

<h2>Description</h2>



<div class="kk-star-ratings kksr-auto kksr-align-center kksr-valign-top" data-payload="{&quot;align&quot;:&quot;center&quot;,&quot;id&quot;:&quot;109916&quot;,&quot;slug&quot;:&quot;default&quot;,&quot;valign&quot;:&quot;top&quot;,&quot;ignore&quot;:&quot;&quot;,&quot;reference&quot;:&quot;auto&quot;,&quot;class&quot;:&quot;&quot;,&quot;count&quot;:&quot;1&quot;,&quot;legendonly&quot;:&quot;&quot;,&quot;readonly&quot;:&quot;&quot;,&quot;score&quot;:&quot;5&quot;,&quot;starsonly&quot;:&quot;&quot;,&quot;best&quot;:&quot;5&quot;,&quot;gap&quot;:&quot;4&quot;,&quot;greet&quot;:&quot;Rate this product&quot;,&quot;legend&quot;:&quot;5\/5 - (1 vote)&quot;,&quot;size&quot;:&quot;24&quot;,&quot;title&quot;:&quot;CS2200 Project 6 Solved&quot;,&quot;width&quot;:&quot;138&quot;,&quot;_legend&quot;:&quot;{score}\/{best} - ({count} {votes})&quot;,&quot;font_factor&quot;:&quot;1.25&quot;}">

<div class="kksr-stars">

<div class="kksr-stars-inactive">
            <div class="kksr-star" data-star="1" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="2" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="3" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="4" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="5" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
    </div>

<div class="kksr-stars-active" style="width: 138px;">
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
    </div>
</div>


<div class="kksr-legend" style="font-size: 19.2px;">
            5/5 - (1 vote)    </div>
    </div>
Read the entire document before starting. There are critical pieces of information and hints along the way.

In this project, you will be implementing a virtual memory system simulator. You have been given a simulator which is missing some critical parts. You will be responsible for implementing these parts. Detailed instructions are in the files to guide you along the way. If you are having trouble, we strongly suggest that you take the time to read about the material from the book and class notes.

There are 10 problems in the files that you will complete. The files that you will be changing are the following:

page_splitting.h – Break down a virtual address into its components. paging.c – Initialize any necessary bookkeeping and implement address translation.

page_fault.c – Implement the page fault handler. page_replacement.c – Write frame eviction and the Counter-Clocksweep algorithm.

stats.c – Calculate the Average Access Time (AAT)

2 Splitting a Page Address

In most modern operating systems, user programs access memory using virtual addresses. The hardware and the operating system work together to turn the virtual address into a physical address, which can then be used to address into physical memory. The first step of this process is to translate the virtual address into two parts: the higher order bits for the VPN, and the lower bits for the page offset.

In page_splitting.h, complete the vaddr_vpn and vaddr_offset functions. These will be used to split a virtual address into its corresponding page number and page offset. You will need to use the parameters for the virtual memory system defined in pagesim.h (PAGE_SIZE, MEM_SIZE, etc.).

3 Memory Organization

The simulator simulates a system with 1MB of physical memory. Throughout the simulator, you can access physical memory through the global variable uint8_t mem[] (an array of bytes called “mem”). You have access to, and will manage, the entirety of physical memory.

The system has a 24-bit virtual address space and memory is divided into 16KB pages.

Like a real computer, your page tables and data structures live in physical memory too! Both the page table and the frame table fit in a single page in memory, and you’ll be responsible for placing these structures into memory.

Note: Since user data and operating system structures such as the frame table and page tables coexist in the same physical memory, we must have some way to differentiate between the two, and keep user pages from taking over system pages.

For this project, we’ll take a simpler approach: Every frame has a “protected” bit, which we’ll set to “1” for system frames and “0” for user frames.

Please reference Section 7.4.1 in your textbook for a more detailed diagram of the user’s view of virtual and physical memory and how they are mapped to each other using the page table.

Figure 1: Organization of physical memory showing frames and frame entries.

4 Initialization

Before we can begin accessing pages, we will need to set up the frame table (sometimes known as a “reverse lookup table”). After that, for every process that starts, you’ll need to give it a page table.

For simplicity, we always place the frame table in physical frame 0. Because we are simulating your hardware using a Linux process, your physical memory will not actually start at address zero. There is a pointer in the simulator named “mem” that contains the address at which your (simulated) physical memory starts. This is of little consequence other than you need to add this base address to the PFN * PAGE_SIZE + offset any time you translate a virtual address to a physical address in your simulated computer hardware.

To set up the frame table, you need to initialize the pointer to the start of the frame table. Remember that this frame table belongs in a frame in memory – the first frame, so the pointer to the start of the frame table is just a frame table entry pointer. Don’t forget to mark this first frame as “protected”. We will never evict the frame table. To do this, we set a protected bit. During your page replacement, you will need to make sure that you never choose a protected frame as your victim.

Since processes can start and stop any time during your computer’s lifetime, we must be a little more sophisticated in choosing which frames to place their page tables in. For now, we won’t worry about the logistics of choosing a frame–just call the free_frame function you’ll write later in page_replacement.c. (Do we ever want to evict the frame containing the page table while the process is running?)

Your task is to fill out the following functions in paging.c:

1. system_init()

2. proc_init()

Each frame contains PAGE_SIZE bytes of data, therefore to access the start of the i-th frame in memory, you can use mem + (i * PAGE_SIZE).

5 Context Switches and the Page Table Base Register

As you know, every process has its own page table. When the processor needs to perform a page lookup, it must know which page table to look in. This is where the page table base register (PTBR) comes in.

In the simulator, you can access the page table base register through the global variable pfn_t PTBR.

Implement the context_switch function in paging.c. Your job is to update the PTBR to refer to the new process’s page table. This function will be very simple.

Going forward, pay close attention to the type of the PTBR. The PTBR holds a physical frame number (PFN), not a virtual address. Think about why this must be.

6 Reading and Writing Memory

Figure 2: Shows when and how disk reading and writitng occurs in the project.

The ability to allocate physical frames is useless if we cannot read or write to them. In this section, you will add functionality for reading and writing individual bytes to memory.

Because processes operate on a virtual memory space, it is necessary to first translate a virtual address supplied by a process into its corresponding physical address, which then will be used access the location in physical memory. This is accomplished using the page table, which contains all of a process’s mappings from virtual addresses to physical addresses.

Implement the mem_access function in paging.c. You will need to use the passed-in virtual address to find the correct page table entry and the offset within the corresponding page. HINT: Use the page splitting functions that you wrote earlier in the project.

Once you have identified the correct page table entry, you must use this to find the corresponding physical frame and its address in memory, and then perform the read or write at the proper location within the page. (Remember that the simulator’s memory is represented by the mem array).

Keep in mind that not all entries in a process’s page table have necessarily been mapped. Entries without a VPN to PFN translation are marked as invalid, and an attempt to access an invalid address should generate a page fault. You will write the page_fault() function in the next section, so for now just assume that it has successfully located a page for that address after it returns.

Make sure to mark the containing page as “dirty” in the process’s page table on a write. These bits will be used later when deciding on what pages should be evicted first, and if an evicted page needs to be written to the disk to preserve its content.

The image at the top of this section is representing the Disk swapping as it occurs in this project specifically. You can find a diagram of how the Disk works in real life in the textbook in section 8.1.3

7 Eviction and Replacement

Recall that when a CPU encounters an invalid VPN to PFN mapping in the page table, it triggers a page fault. The page fault handler in the OS allocates a new frame for the page by either finding an empty frame or evicting a page from a frame that is in use. In this section, you will be implementing a page fault and replacement mechanism.

Implement the function page_fault() in page_fault.c. A page fault occurs when the CPU attempts to translate a virtual address, but finds no valid entry in the page table for the VPN. To handle the page fault, you must find a frame to hold the page (call free_frame()), then update the page table and frame table to reference that frame.

Next, we will turn our attention to the eviction process in page_replacement.c.

If you ask the system for a free frame when all the frames are in use, the operating system must select an in-use frame and re-use it, “evicting” any existing page that was previously using the frame. Implement this logic in free_frame(). To resolve the page fault, you must do the following:

1. Mark the mapping within the evicted process’ page table as invalid.

2. Unmap the corresponding frame table entry.

3. Update the mapping from VPN to PFN in the current process’ page table.

4. If the page has been swapped out previously (meaning it has been evicted before), read the swapped-out version into the frame; otherwise, fill the frame with zeroes.

There is an additional field in the PTE called swap in which we keep the disk logical block number where the page is swapped out. Once a page is swapped out, it keeps its disk block until the virtual address space is freed at process-end. The simulator uses a obscured linked list to simulate the hard disk drive; swapped pages are copied into the linked list instead of being physically written to a disk block, but that substitute implementation isn’t visible to your code in the simulator.

Swap space effectively extends the memory of your system. If physical memory is full, the operating system kicks some frames to the hard disk to accommodate others. When the “swapped” frames are needed again, they are restored from the disk into physical memory. Since accessing the disk is very slow, we try to avoid it as much as possibly by only writing/reading from the disk when needed.

8 Finishing a Process

If a process finishes, we don’t want it to hold onto any of the frames that it was using. We should release any frames so that other processes can use them. Also: If the process has finished executing, can we release the page table?

As part of cleaning up a process, you will need to also free any swap entries that have been mapped to pages.

You can use swap_free() to accomplish this. Implement the function proc_cleanup() in paging.c.

9 Better Victim Selection

In section 7, we relied on the select_victim_frame() function to tell us which frame to choose as our

“victim”.

We have provided you with a default, inefficient page replacement algorithm that randomly selects a page to be evicted. The simulator can run this replacement strategy out-of-the-box so that you can test the other parts of your code without having to write a page replacement algorithm. Run the simulator with -rrandom to use the random algorithm.

Of course, we can do better than random replacement. We will have you implement a modified clocksweep (or second chance) algorithm called counter-clocksweep. Every frame table entry has a referenced bit which is set when the associated frame is accessed. The counter-clocksweep algorithm wills start with the bottom of the frame table, iterating backwards, and choose the first frame you come across that does not have its referenced bit set to 1 as the victim. Once you get to the beginning of the frame table, you should circle back to the end and continue searching. Along the way, it will clear any set referenced bits – in other words, if an encountered frame’s referenced bit is set, your counter-clocksweep algorithm will clear it. Your algorithm should search for the frames in a circular counter-clockwise fashion, resuming where it left off with each subsequent call. Look at section 8.3.5 in the textbook for more information on this.

Remember again that if the protected bit is set, it should never be chosen as a victim frame.

Once you have implemented the Counter-Clocksweep algorithm, you will be able to run the simulator with the -rcounterclocksweep argument to use the algorithm as your page replacement strategy. Once you write your stats function in section 10, compare the performance of the two algorithms. What do you observe?

10 Computing AAT

In the final section of this project, you will be computing some statistics.

writes – The total number of accesses that were writes reads – The total number of accesses that were reads accesses – The total number of accesses to the memory system page faults – Accesses that resulted in a page fault writebacks – How many times you wrote to disk aat – The average access time of the memory system

We will give you some numbers that are necessary to calculate the AAT:

MEMORY READ TIME – The time taken to access memory SET BY SIMULATOR

DISK PAGE READ TIME – The time taken to read a page from the disk SET BY SIMULATOR

DISK PAGE WRITE TIME – The time taken to write to disk SET BY SIMULATOR

You will need to implement the compute_stats() function in stats.c

11 Simulator Process Diagram

Figure 3: This diagram gives a general overview of how the simulator works.

12 How to Run / Debug Your Code

12.1 Environment

12.2 Compiling and Running

We have provided a Makefile that will run gcc for you. To compile your code with no optimizations (which you should do while developing, it will make debugging easier) and test with the “random” algorithm, run:

$ make

$./vm-sim -i traces/&lt;trace&gt;.trace -rrandom

Once your Counter-Clocksweep algorithm has been implemented, you can run the program with the -rcounterclocksweep argument in order to test. For example, you should run:

$ make

$./vm-sim -i traces/&lt;trace&gt;.trace -rcounterclocksweep

We highly recommend starting with “simple.trace.” This will allow you to test the core functionality of your virtual memory simulator without worrying about context switches or write backs, as this trace contains neither.

12.3 Corruption Checker

One challenge of working with any memory-management system is that your system can easily corrupt its own data structures if it misbehaves! Such corruption issues can easily hide until many cycles later, when they manifest as seemingly unrelated crashes later.

To help with detecting these issues, we’ve included a “corruption check” mode that aggressively verifies your data structures after every cycle. To use the corruption checker, run the simulator with the -c argument:

$./vm-sim -c -i traces/&lt;trace&gt;.trace -r&lt;algorithm&gt;

12.4 Debugging Tips

If your program is crashing or misbehaving, you can use GDB to locate the bug. GDB is a command line interface that will allow you to set breakpoints, step through your code, see variable values, and identify segfaults. There are tons of online guides, click here (http://condor.depaul.edu/glancast/373class/docs/gdb.html) for one.

To compile with debugging information, you must build the program with make debug:

$ make clean

$ make debug

To start your program in gdb, run:

$ gdb ./vm-sim

Within gdb, you can run your program with the run command, see below for an example:

$ (gdb) r -i traces/&lt;trace&gt;.trace -r&lt;algorithm&gt;

$ (gdb) break pagesim.c:53 ! set breakpoint at call to system_init

$ (gdb) r -i traces/&lt;trace&gt;.trace -r&lt;algorithm&gt;

! (wait for breakpoint)

$ (gdb) s ! step into the function call

or by using the actual function name being called from the main loop:

$ (gdb) break sim_cmd ! set breakpoint at call to sim_cmd

$ (gdb) r -i traces/&lt;trace&gt;.trace -r&lt;algorithm&gt;

! (wait for breakpoint)

$ (gdb) s ! step into the function call

$ (gdb) x/24xb frame_table

0x1004000aa: 0x00 0x00 0x00 0x00 0x00 0x00 0x00 0x00

0x1004000b2: 0x00 0x00 0x00 0x00 0x00 0x00 0x00 0x00

0x1004000ba: 0x00 0x00 0x00 0x00 0x00 0x00 0x00 0x00

The format of this command is x/nfu [memory location], where n is the number of items to print, f is a formatting identifier (for example, x for hexadecimal), and u is the specifier for the units you would like to print. b specifies units of 1 byte, h specifies 2 bytes, w specifies 4 bytes, and g specifies 8 bytes. So, our above command showed us 24 bytes of memory starting at frame_table in hexadecimal form.

If you use the corruption checker, you can set a breakpoint on panic() and use a backtrace to discover the context in which the panic occurred:

$ (gdb) break panic

$ (gdb) r -i traces/&lt;trace&gt;.trace -r&lt;algorithm&gt;

! (wait for GDB to stop at the breakpoint)

$ (gdb) backtrace

$ (gdb) frame N ! where N is the frame number you want to examine

12.5 Verifying Your Solution

On execution, the simulator will output data read/write values. To check against our solutions, run

$ ./vm-sim -i traces/&lt;trace&gt;.trace -rcounterclocksweep &gt; my_output.log

$ diff my_output.log outputs/&lt;trace&gt;.log

$ ./vm-sim -i traces/astar-random.trace -rrandom &gt; my_output.log

$ diff my_output.log outputs/astar-random.log

13 How to Submit

Run make submit to automatically package your project for submission. Submit the resulting tar.gz zip on Canvas.

Always re-download your assignment from Canvas after submitting to ensure that all necessary files were properly uploaded. If what we download does not work, you will get a 0 regardless of what is on your machine.

This project will be demoed. In order to receive full credit, you must sign up for a demo slot and complete the demo. We will announce when demo times are released.
