| Feature                                            | **Valgrind**                                         | **AddressSanitizer (`-fsanitize=address`)** |
| -------------------------------------------------- | ---------------------------------------------------- | ------------------------------------------- |
| **Instrumentation**                                | Runs the program in an emulated environment          | Uses compiler instrumentation               |
| **Performance**                                    | **Slow** (interprets instructions, ~10-20x slowdown) | **Fast** (~2x slowdown)                     |
| **Memory Overhead**                                | High                                                 | Moderate                                    |
| **Detects Use-After-Free**                         | Yes                                                  | Yes                                         |
| **Detects Heap Buffer Overflow**                   | Yes                                                  | Yes                                         |
| **Detects Stack Buffer Overflow**                  | Limited                                              | Yes                                         |
| **Detects Leaks**                                  | Yes (via `--leak-check=full`)                        | Yes (`-fsanitize=leak`)                     |
| **Detects Uninitialized Reads**                    | Yes (`--track-origins=yes`)                          | No                                          |
| **Detects Unclosed File Descriptors & Semaphores** | **Yes**                                              | **No**                                      |
| **Detects Unmapped Memory Access**                 | Yes                                                  | Yes                                         |

## Valgrind Options
`--trace-children=yes` - tracks child porcesses
`--leak-check=full`

## Fsanitize Options
`-fsanitize=leak`
`-fsanitize=thread`
`-fsanitize=address`
`-fsanitize=memory` (only available )