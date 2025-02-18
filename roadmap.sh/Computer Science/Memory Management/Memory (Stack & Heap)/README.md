## Stack vs Heap

- **Value Types**
    - Stored in the **stack** when inside a function.
    - Stored in the **heap** if global or inside a class.
- **Reference Types** (anything with a pointer) & **Static Variables**
    - Always stored in the **heap**.

## How Garbage Collection Works
- The garbage collector **removes unused objects** in the heap.
- If a reference no longer points to an object, the object is **collected and deleted** automatically.


