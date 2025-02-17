- Contiguous - Adjacent to each other

# Contiguous Memory Allocation 
- available memory space is resided together and not distributed in a random manner
- main memory is a combination of two portions, one for the operating system and another for the user program
- this method of allocation can be achieved by dividing the free memory into fixed size partitions

# Non-contiguous memory
- available memory space is distributed and scattered
- helps reduce memory wastage, eventually giving rise to internal and external memory fragmentation
	- **Fragmentation** 
		- process which storage space is used inefficiently, reducing capacity and performance
	- **Internal Fragmentation** 
		- a fixed-sized partition is not fully utilized by a process (eg: 32kb memory only used by 30kb process, 2kb remaining)
	- **External Fragmentation** 
		- free memory is scattered throughout the system, leading to a scenario when there is enough total memory to satisfy a process, but it is not contiguous and large enough (eg: 10kb, 20kb, but a 15kb process cannot be allocated eventhough there is total 30kb), usually occurs after many rounds of allocation and deallocation