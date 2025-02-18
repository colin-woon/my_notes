## Processes and Memory Allocation
#### - A program (containing code), is an executable, that when loaded into memory, and executed by the processor, becomes a process.

A **process** has its own **memory address space**, which is divided into different sections:
1. **Stack** – Stores local variables, function calls, and control flow
2. **Heap** – Stores dynamically allocated memory (e.g., `malloc`, `new`).
3. **Code** – Stores the program’s instructions.
4. **Data (Static & Global)** – Stores global and static variables.

## Threads and Memory Allocation
#### - A thread is a unit of execution within a process, and each process has at least one thread, that is the main thread

- **Each thread** within a process has its **own stack**.
- **All threads share the same heap** (since they belong to the same process).
