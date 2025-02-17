# Segmentation fault (SIGSEGV, Segmentation Violation, signal 11)
- Segmentation refers to memory segmentation concept, a system level feature in computer architectures that divides computer memory into different segments with its own set of permission and boundaries
- program tries to read/write outside the memory allocated for it, or writing memory which can only be read.
- Occurs when:
	- using uninitialiazed pointer `char *ptr;`
	- de-referencing NULL pointer `*(*ptr)`
	- trying to access an array element out of array bounds
	- trying to access deallocated memory
# Bus Error (SIGBUS, signal 10)
- Bus refers to how data bus in computer system handles memory access, its a communication system that transfers data between components
- the memory is accessed in a way where the CPU hardware cannot physically support 
- Occurs when:
	- memory doesnt physically exist
	- unaligned memory access
	- trying to modify a read-only memory (See [[String Literal Memory]])


# Main Difference between SIGSEGV & SIGBUS
- SIGSEGV invalid access to valid memory
- SIGBUS access to invalid address
