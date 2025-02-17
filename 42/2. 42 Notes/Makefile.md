### How to use
- `make <rule_name>` -- if rule name is empty, runs `all`, else will run whatever command is defined in the rule
### Automatic Variables
**#EXAMPLE MAKEFILE (BEFORE)**
```
{target} : {dependency}
all : test.exe

test.exe : main.o test.o
	gcc main.o test.o -o test.exe

main.o : main.c
	gcc main.c -c -o main.o

test.o : test.c
	gcc test.c -c -o test.o
```

- **`$@` - refers to target**
```
test.exe : main.o test.o
	gcc main.o test.o -o {test.exe OR $@}
```

- **`$^` - replaces all prerequisites/dependencies (without duplicate)** 
```
test.exe : main.o test.o
	gcc {main.o test.o OR $^} -o $@

main.o : main.c
	gcc $^ -c -o main.o
```

- **`$<` - replaces FIRST prerequisite/dependency**
```
test.exe : main.o test.o
	gcc {main.o OR $<} test.o -o $@

main.o : main.c
	gcc $< -c -o main.o
```

- **`$+` - replaces all prerequisites/dependencies (with duplicate)** 
```
test.exe : main.o test.o test.o (duplicate here)
	gcc $+ -o $@   ## WILL THROW AN ERROR

main.o : main.c
	gcc $+ -c -o main.o  ## WORKS FINE
```

- **`$?` - replaces only with newer prerequisites** 
```
test.exe : main.o test.o
	gcc $^ -o $@
	echo $?

USECASE:
- run "make"
- rm -rf main.o/test.o
- run "make" again
- it will show which file was newly generated again, compared to the TARGET
```



**#EXAMPLE MAKEFILE (AFTER)**
```
{target} : {dependency}
all : test.exe

test.exe : main.o test.o
	gcc $+ -o $@
	echo $?

main.o : main.c
	gcc $< -c -o $@

test.o : test.c
	gcc $^ -c -o $@
```


### File Structure Example
```
VARIABLE_NAME = value
${VARIABLE_NAME} = value

SRCS = srcs/ft_putchar.c \ srcs/ft_putnbr.c
OBJS = ${SRCS:.c=.o}
INCS = includes
NAME = libft.a
LIBC = ar rc
LIBR = ranlib
CC = gcc
RM = rm -f
CFLAGS = -Wall -Wextra -Werror -c

${NAME}: ${OBJS}
	${LIBC} ${NAME} ${OBJS} //ar rc libft.a *.o
	${LIBR} ${NAME} //used to generate index to speed up library, but not popular

%.o: %.c
	${CC} ${CFLAGS} $< -o ${<:.c=.o} -I ${INCS}

all: {NAME} //run by default

clean:
	${RM} ${OBJS}

fclean:
	${RM} ${NAME}

re: fclean all
```