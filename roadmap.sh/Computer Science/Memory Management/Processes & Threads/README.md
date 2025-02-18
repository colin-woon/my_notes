## Processes and Memory Allocation

A **process** has its own **memory space**, which is divided into different sections:
1. **Stack** – Stores local variables, function calls, and control flow
2. **Heap** – Stores dynamically allocated memory (e.g., `malloc`, `new`).
3. **Code** – Stores the program’s instructions.
4. **Data (Static & Global)** – Stores global and static variables.

## Threads and Memory Allocation
- **Each thread** within a process has its **own stack**.
- **All threads share the same heap** (since they belong to the same process).
