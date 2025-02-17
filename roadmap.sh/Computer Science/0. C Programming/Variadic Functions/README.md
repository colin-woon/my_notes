# Variadic Functions
## Vocabulary
	va - vector  arguments
	ap - argument pointer
	... - ellipsis
	macro - essentially a form of text substitution, where the preprocessor replaces the macro with its defined value or code.

## stdarg library macros
- `va_list` for declaring a variable to hold the arguments, usually named as `ap`
- `va_start({va_list ap}, {last arg})` to initialize the argument list `ap`.
- `va_arg({va_list ap}, {arg type})` to retrieve each argument, `arg type` literally refers to `int, char` etc
- `va_end` to clean up.

## Example
```
int total(int number_of_additions, ...)
{
	va_list ap;
	int total;
	int i;

	total = 0;
	va_start(ap, number_of_additions);
	while (i < number_of_additions)
	{
		total += va_args(ap, int)
		i++;
	}
	va_end(ap);
	return (total);
}
```

- `...` - uses *default argument promotion* 
- When a function's definition or declaration does not specify the type of an argument, that argument is passed without conversion in whatever type it has, except:
	- *narrow numeric values* will be promoted to *wider numeric values*
		- eg: `char or short` convert to `int`
	- `float` to `double`
	- **an array as argument is converted to a pointer to its 0th element**
	- function name as argument is converted to a pointer to that function

## See other example in [[2. ft_printf]]
