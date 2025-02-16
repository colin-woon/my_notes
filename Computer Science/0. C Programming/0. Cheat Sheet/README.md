# APPLIED IN 42

**(Check custom alias in .zshrc file in ~)**
# 42 header
- vim - f1
- vscode - 42header extension

# Norminette Command
- norm = "norminette -R CheckForbiddenHeaderSource"
- normh = "norminette -R CheckDefine"

# Compiling 
**You need a int main() function to compile, so uncomment it for testing and comment it before you hand in your work!**
- compile = "gcc -Wall -Wextra -Werror"
- gcc - GNU Compiler
- -Wall -- enables base set of warning options
- -Wextra -- enables additional warning options not covered by -Wall
- -Werror -- treats all warnings as errors, ensures file compiles without warnings
- -o -- renames .out file
- How to use: -> compile -o newprogram source1.c source2.c
- -c -- creates an object file .o
- How to use: -> compile -c -o newprogram.o source1.c source2.c
**Once a.out file generated, can use alias:**
- run = "./a.out && rm ./a.out"


# General Syntax and Rules
- 'x' --integer, representing the ascii code
- "x" --string literal, contains 2 chars (x & \\0, the null terminator)
- void function_name -- no return value
- void \*function_name -- returns a pointer to the modified memory block 
	 - void\* is a generic pointer that points to ANY data type
	 - useful for memory allocation or manipulation functions
	 - must type cast into `char *` to perform array subscripting or pointer arithmetic as compiler doesnt know the size of data that void* is pointing to, different data types like int, long, float, and char has different bytes and sizes.
	 - typecasting into `char *` doesnt necessarily mean its a string, its just to perform pointer arithmetic
- type function_name -- return type_value
- type \*function_name -- returns a pointer value
- use `\` if line too long 
- Pointer
	- var = 1
	- &var = memory address of var = mem
	- \*mem = **pointer** to memory address of var = 1 
	- if mem++, memory address of var is being incremented, then \*mem will display new value, probably the integer 2 in the ascii table
	- See [[#Pointer Syntax for linked list]]
- Integer promotion:
	- Types smaller than `int`, such as `char`, `signed char`, `unsigned char`, `short`, and `unsigned short`, are promoted to `int` if all values of the original type can fit into an `int`. Otherwise, they are promoted to `unsigned int`
	- When a `char` or `short` is used in an expression, it is converted to `int` or `unsigned int` before the operation.
	- Applies to other things like `double`, `float` too
- Vocabulary
	- Function Declaration/Prototype - `int add (int a, int b);`
	- Argument Expression - `int result = add(5, 10)` *(5&10 are the expressions)* 
	- Function Definition - `int add (int a, int b) {return (a+b)}`


# Arguments
- int main(int argc, char \*argv\[])
	- argc -- argument count, including the name of the program itself 
		- (eg: ./program arg1 arg2, argc = 3)
	- \*argv\[] -- array of pointers, most correct way to declare argv argument in main function
		- (eg: argv\[0] is the name of the program)
		- argv\[argc] will always refer to null pointer, end of the argument list

# Structure
```
typedef struct student { // struct tag `student` (Optional)
	char name[50]; 
	int age; 
	float gpa; 
}; scholar // type alias

struct student john, mary;
john.age = 20; 
mary.gpa = 3.8

scholar colin;
colin.age = 22;
colin.gpa = 4.0;
```
- Declaring a struct doesn't allocate memory. You need to create variables to use it.
- Structs can contain other structs as members for more complex data organization.
- You can use `sizeof` operator to find the total size of a struct in bytes.
- `type alias` allows you to declare variables of type `scholar` instead of having to use `struct student` each time.
- See [[#Structure Self Referential Structure|Self Referential Structure]]

# Header files (library)
```
//typical naming convention and practice
//USE normh alias to check formatting
//instead of boilerplate #ifndef, can also use #pragma once, but might run into issues with older compilers

#ifndef FILENAME
#define FILENAME 

typedef struct
{
	int x;
	int y;
} t_point;

int add(int v, int w); (function interface/prototype)

#define ONE_LINE_FUNCTION (MACROS)

#endif
```
- Typically there are at least 3 files to utilize a library
	- `main.c` *(calls the function)*
	- `library.c` *(contains the implementation/code of the functions)*
	- `library.h` *(contains the interface of the functions)*
- To use custom libraries, `#include "library.h"` in the file you want to use, in this case `main.c`, then compile using `gcc -o program_name main.c library.c`, then run `./program_name` to execute **(REMEMBER TO WRITE `#include "library.h"` IN BOTH .c FILES!)**

# Object files (.o)
- Created before the GNU compiler creates the executable file a.out (name by default)
- The linker will link all object files to create the executable file.
- How to use:
	- Command: `gcc -c main.c library.c`
	- Output: `main.o library.o`
	- If any changes made to either file, just recompile again with `-c` flag to get the object file
	- If no changes, run `gcc -o program main.o library.o` to create and run your executable `program`
- Useful when you just want to make changes to one file, you wont have to recompile everything again, instead just recreate the object file of the updated code.
- See [[#Makefile]] to learn how to automate and write scripts to streamline the process


# Static library (.a)
- `ar rcs library_name.a *.o`
	- `ar` -- archive, creates and manipulates static libraries
	- `r` -- replace or add files to archive
	- `c` -- create the archive if it doesnt exist
	- `s` -- updates the symbol table of the archive (important for linker to identify changes made in libary)
- All object files are usually deleted after the library is created.
- Usecase:
	- `gcc -o program file_code.c -L{/path/to/library} -l{library_name}`
	- `-l` already includes `lib` and `.a` extension, so if library name is `libft.a`, `-lft` also works



# Functions as parameters
```
void delete_content(void *content) //A
{ 
	free(content);
}

void ft_lstdelone(t_list _lst, void (del)(void *)) //B
{ 
	if(lst == NULL || del == NULL) 
		return ; 
	(del)(lst->content); //specified here
	free(lst); 
}

SYNTAX
[  void      (del)(void *)      ]
[    |         |      |         ]
[  return  function function    ]
[  type      name   param type  ]

ft_lstdelone(node, delete_content);

*delete_content is the function passed*
```
- When the `function A` is passed as a parameter in `function B`, only its **parameter types** are required to be stated. Meanwhile the parameters for the passed `function A` is already specified in the `function B` that called it. In this case, `*content = lst->content` 

# Linked Lists
- Array is a sequential representation of linked lists (means in sequence)
- Linked list is the linked representation of a list (shows its link, eventhough not in sequence in memory context)
- Example Array and Linked List:
	- int is 4 bytes
	- theres an int `1` at memory address `1000`
	- int `2` is at memory address `1004` and so on...... This is ARRAY
	- As for linked list, memory address of `2` could be `452` `(any random address < 1000)`, and `1` can still be linked to `2` in the list, meaning itll still be `1, 2`
- A `node` of a linked list represents the `data` and `link`
```
+---------+----------+      +---------+----------+
|  Data   |   Link   | ---> |  Data   |   Link   |
+---------+----------+      +---------+----------+
      |         |               |
      v         v               v
    Node   Mem address       Another Node
           of next node 
```
##### [[#Structure |Self Referential Structure]]
- this is required to create a node
- it contains a pointer pointing to a structure of the same type
```
struct node {
	int data;
	struct node *link;
}
```
## Pointer Syntax for linked list
- if `**var`, visualize it as `*(*var)`, then dereference that variable to see its value, and also remember that pointers always point to 1 single item only, so if you just pass `var` into a function and if `var` is a list/array, it will reference to the ***nth*** element that it is at, so pass in `&var` to represent the entire list/array
		- `t_list *var = [{file_buffer}, {next_node}]` *(for visualisation purpose)* 
		- `func(t_list **ptr_to_var);` *(prototype)*
		- `func(var)` *(will represent var\[0], which is a single node ONLY, this is incorrect)*
		- `func(&var)` *(will represent the actual variable itself, \*var containing all nodes)*
		- In the `func(t_list **ptr_to_var)`:
```
			 **ptr_to_var = &var 
			 *ptr_to_var = var (contents of node) 
			 (var->file_buffer  OR  (*ptr_to_var)->file_buffer)
			 ptr_to_var = *var (the node)
```
# fsanitse & valgrind
gcc -fsanitise=address -g3 (for mac)

gcc get_next_line.c get_next_line_utils.c -Wall -ggdb3 -std=c11
valgrind -s --leak-check=full ./a.out
