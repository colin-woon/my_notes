# Time Complexity
- Criteria:
	- can compared number of basic operations required to do something
## Big O notation
- finds the worst case scenario, and gives an upper bound to the growth rate of the algorithm
- eg: In this algorithm's worst case, it will not grow faster than \<Big O Notation\>

| Big O Notation | Growth Description                                                    | Example Algorithm                             |
| -------------- | --------------------------------------------------------------------- | --------------------------------------------- |
| **O(1)**       | Constant time, doesn't change with input size                         | Accessing an element in an array              |
| **O(n)**       | Linear time, grows directly with input size                           | Simple for loop, Linear Search                |
| **O(log n)**   | Logarithmic time, grows slower than input size                        | Binary Search                                 |
| **O(n log n)** | Linearithmic time, grows faster than linear but slower than quadratic | Merge Sort, Quick Sort (average case)         |
| **O(n²)**      | Quadratic time, grows quickly as input size increases                 | Bubble Sort, Selection Sort                   |
| **O(n³)**      | Cubic time, grows even faster than quadratic                          | Matrix Multiplication with three nested loops |
| **O(2ⁿ)**      | Exponential time, doubles with each additional input                  | Recursive solutions to the Tower of Hanoi     |
| **O(n!)**      | Factorial time, growth explodes as input increases                    | Brute-force Traveling Salesman Problem        |

- ![[Pasted image 20240821175432.png]]
- ![[Pasted image 20240821175459.png]]
- ![[Pasted image 20240821175342.png]]
- ![[Pasted image 20240821175612.png]]
- ![[Pasted image 20240821180033.png]] In this case, its O(n) for the **else** part, as the if part is constant **O(1)**
- ![[Pasted image 20240821182759.png]]![[Pasted image 20240821182828.png]]

