## Stack vs Heap

- **Value Types**
    - Stored in the **stack** when inside a function.
    - Stored in the **heap** if global or inside a class.
- **Reference Types** (anything with a pointer) & **Static Variables**
    - Always stored in the **heap**.

## How Garbage Collection Works
- The garbage collector **removes unused objects** in the heap.
- If a reference no longer points to an object, the object is **collected and deleted** automatically.

### How Stack Works
- Each function call creates a **new stack frame**.
- When the function returns, the stack frame is **popped** (deleted).
- **Fast and efficient** since memory is managed automatically.

### How Heap Works
- Used for **dynamic memory allocation** (e.g., `malloc`, `new`).
- Must be manually freed (`free`, `delete`) or handled by a **garbage collector**.
- **Slower than the stack** because allocation and deallocation take time.
- Shared across threads (async methods), so **synchronization (e.g., mutexes) is needed** to prevent issues.


