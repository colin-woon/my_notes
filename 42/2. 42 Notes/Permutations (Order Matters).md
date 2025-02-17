The formula to calculate the number of permutations of `r` objects chosen from a set of `n` distinct objects is given by:

![[Pasted image 20240829154558.png]]

where:

- `P(n, r)` represents the number of permutations.
- `n` is the total number of distinct objects.
- `r` is the number of objects selected.
- `!` denotes the factorial of a number.

**Example:** If you have 3 numbers (say 1, 2, 3) and want to arrange them in all possible orders, the number of permutations is: P(3,3)=3!(3−3)!=6P(3, 3) = \frac{3!}{(3-3)!} = 6P(3,3)=(3−3)!3!​=6
- **Example:** Let's consider 3 numbers and arrange them in all possible orders.
    - Possible permutations:
        1. (1, 2, 3)
        2. (1, 3, 2)
        3. (2, 1, 3)
        4. (2, 3, 1)
        5. (3, 1, 2)
        6. (3, 2, 1)
    - Total number of permutations: 6

In summary:

- **Combinations without repetition:** {1,2},{1,3},{2,3}\{1, 2\}, \{1, 3\}, \{2, 3\}{1,2},{1,3},{2,3}
- **Combinations with repetition:** {1,1},{1,2},{1,3},{2,2},{2,3},{3,3}\{1, 1\}, \{1, 2\}, \{1, 3\}, \{2, 2\}, \{2, 3\}, \{3, 3\}{1,1},{1,2},{1,3},{2,2},{2,3},{3,3}
- **Permutations:** (1,2,3),(1,3,2),(2,1,3),(2,3,1),(3,1,2),(3,2,1)(1, 2, 3), (1, 3, 2), (2, 1, 3), (2, 3, 1), (3, 1, 2), (3, 2, 1)(1,2,3),(1,3,2),(2,1,3),(2,3,1),(3,1,2),(3,2,1)