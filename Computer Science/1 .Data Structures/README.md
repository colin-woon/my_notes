# Data
![[Pasted image 20240821155253.png]]
- Example: `c = a + b`

# Information
- Given when data is sorted in a systematic way

# Data Structure
- A systematic way to organize data so it can be used efficiently
## Types
- Arrays (Stores bitmap images)
- Stacks (Undo & Redo)
- Graph (Storing friend connections in Social Media)
- Linked List
- Circular Buffer

# Abstract Data Type (ADT)
- blueprint for user-defined datatype (eg: structs, union)
## Dictionary Definition
- A model for a certain kind of data structure that specifies the behavior of the data type from the point of view of a user, in terms of possible operations (like insertion, deletion, or access) and their expected effects, without specifying how these operations are implemented.
- **ADT tells us what needs to be done and data structures tells us how to do it**
- ***eg: stack ADT can be implemented with array or linked list***
	- different implementations of ADT are compared with time and space efficiency

# Linear Data Structure
- all elements are arranged in sequential order
- typically each element have 1 predecessor and 1 successor
- eg:
	- Stacks
	- Array
	- Linked List
	- Queue

# Non-Linear Data Structure
- arranged in non-sequential order
- does not follow 1 predecessor and 1 successor rul
- eg:
	- Tree
	- Graph

# Static Data Structure
- memory allocated at **compile time**, maximum size is fixed
- + fast access
- -  slower insertion and deletion
- eg: array

# Dynamic Data Structure
- memory allocated at **run time**, maximum size is flexible
- + faster insertion and deletion
- - slower access
- eg: linked list

# Asymptotic Analysis
- A method of describing the behavior of algorithms as the input size grows arbitrarily large
[[Time Complexity & Big O notation]]