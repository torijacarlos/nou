# Windows

======================================================================================================

## Mysteries of Memory Management Revealed

tags: #windows #memory #talks

[1/2](https://www.youtube.com/watch?v=TrFEgHr72Yg)

Windows is a demand-paged memory system
- Demand: Process aren't born with all the needed resources. They
  demand/request them
    - When a process allocates Virtual Memory, it is just a concept until the
      process actually needs for something physical it can us
- Paged: The granularity of the memory to be handled. Depends on the hardware, but usually is 4KB
    - There are Large pages depending on architecture. (x86: 4MB | x64 and x86 PAE: 2MB)
- There is no memory swapping in windows
- Allocations must happen in 64 kb boundaries. If you allocate just one page, 60KB are wasted
- VirtualMemory and PhysicalMemory have (almost) no connection

### Address Space

* What is an Address space 
Range of virtual addresses that the operating system assigns to a process. This
is the area of contiguous virtual addresses available for executing
instructions and storing data.

The range of virtual addresses in an address space starts at zero and can
extend to the highest address permitted by the operating system architecture.
[Source](https://www.ibm.com/docs/en/zos-basic-skills?topic=storage-what-is-address-space)

**32bit x86 Address Space**

32bit -> 2^32 -> 4 GB
- Memory is splitted in 
    - 2 GB Process Space
    - 2 GB System Space
- Setting 3GT mode (Needs to be Large address space aware)
    - 3 GB Process Space
    - 1 GB System Space

**64bit x86 Address Space**

64bit -> 2^64 -> 17,179,869,184 GB

Processors can't handle that yet.

- x64 today (2016) supports 48 bits
- IA-64 today (2016) supports 50 bits
- 64 bit Windows today (2016) supports 44 bits = 16 TB

- Memory is splitted in 
    - 8 TB Process Space
    - 8 TB System Space
- For 32bit processes on x64
    - 4 GB Process Space
    - 8 TB System Space

Every address space can be:
- Committed: In use. It is actually doing something
- Reserved: Reserved for future use. Can be committed later. Cannot be allocated again.

Every address space is divided in 3
- Private: Used by the process (ie. the heap)
- Shared: Shared memory, DLLs
- Free: Undefined

[VMMap](https://learn.microsoft.com/en-us/sysinternals/downloads/vmmap)


[2/2 (Physical Memory)](https://www.youtube.com/watch?v=RsQyc4xiJeo) *haven't seen 👀*

======================================================================================================

## DirectSound

tags: #audio #directsound #cpp

[IDirectSoundBuffer](https://learn.microsoft.com/en-us/previous-versions/windows/desktop/mt708923(v=vs.85))

According to the docs, there is no need to create a primary buffer. 

First of all, I'm messing up the write process to the audio buffer, so let's go
back to some basics. We are using a Cyclic buffer 

