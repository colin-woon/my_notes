# C++98 Coding Guidelines

## General Requirements

- Your code must comply with the **C++98** standard.
- You are **allowed** to use almost everything from the standard library.
- **C++11** (and derived forms) and **Boost** libraries are **forbidden**.
- The following functions are **forbidden**:
    - `*printf()`
    - `*alloc()`
    - `free()`
- Violating any of these restrictions will result in a **grade of 0**.

## File Naming Conventions

- Class names must follow the **UpperCamelCase** format.
- Files containing class code must be named accordingly:
    - `ClassName.hpp` / `ClassName.h` (header files)
    - `ClassName.cpp` (source files)
    - `ClassName.tpp` (template implementation files, if applicable)
- Example:
    - If a class **BrickWall** represents a brick wall, its header file must be named **BrickWall.hpp**.

## Output Rules

- Every output message must:
    - End with a **new-line character** (`\n`).
    - Be displayed to the **standard output**.

## Memory Management

- When allocating memory using `new`, you **must prevent memory leaks**.

## STL and Algorithm Restrictions

- **Until Module 08:** You **cannot** use:
    - **Containers** (`vector`, `list`, `map`, etc.).
    - **Algorithms** (anything requiring an additional header).
- In **Module 08 and 09**, you are allowed to use the STL.
- Violating these restrictions will result in a **grade of -42**.

## Code Structure and Organization

- Your classes must follow the **Orthodox Canonical Form** (from Module 02 to Module 09).
- **Header Files**:
    - Function implementations in a header file (except for **function templates**) will result in a **grade of 0**.
    - Headers should be **self-contained** (i.e., include all their dependencies).
    - Prevent double inclusion using **include guards** (`#ifndef`, `#define`, `#endif`).
    - Missing include guards will result in a **grade of 0**.