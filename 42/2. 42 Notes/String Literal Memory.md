```
char *str = "Hello"
ft_strrev("Hello")
ft_strrev(str)
```
- All of these ways contains a string literal. These are typically stored in read-only memory, any attempt to modify them will result in bus error.


```
char str[6] = "Hello"
char str[] = "Hello"
char *str = malloc(6);
strcpy(str, "Hello")
ft_strrev(str);
free(str)
```
- To modify the string's value, we can allocate a char array or dynamically allocate memory to it, then pass in the variable as argument to the function