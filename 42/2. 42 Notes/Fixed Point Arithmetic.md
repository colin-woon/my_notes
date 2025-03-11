# **WHAT**
Fixed-point arithmetic is a technique used to represent fractional numbers using integers and bitwise operations. It is commonly used in systems without floating-point units (FPUs) for better performance and precision control.

### What Happens Without an FPU?
Some embedded systems (like low-power microcontrollers) **don’t have an FPU**. In these cases:
- Floating-point operations must be done using **software emulation**, which is **much slower** than hardware-based calculations.
- Instead of floating-point, developers use **fixed-point arithmetic**, which treats fractions as integers using **bit shifting**.

```cpp
static const int fractionalBits = 8;
int fixedA = 1.5 * (1 << fractionalBits);  // 1.5 * 256 = 384
int fixedB = 2.5 * (1 << fractionalBits);  // 2.5 * 256 = 640

// Multiply and shift back
int fixedResult = (fixedA * fixedB) >> fractionalBits; // (384 * 640) >> 8
float finalResult = (float)fixedResult / (1 << fractionalBits);

std::cout << "Fixed-point result: " << finalResult << std::endl;
```

# **HOW**
## Scaling Factor Considerations

Fixed-point arithmetic allows **any** scale factor, but if the scale is a **power of 2**, we can optimize calculations using **bitwise shifting**.

### ✅ Power of 2 Scale (e.g., 2, 4, 8, 16, ...)
- Use **bitwise shift** (`<<` for multiplication, `>>` for division).
- More efficient than normal multiplication and division.

#### Example (Power of 2 Scale):
```cpp
#include <iostream>

int main() {
    float x = 3.75;
    int scale = 1 << 8; // 2^8 = 256

    int fixed_x = static_cast<int>(x * scale); // 3.75 * 256 = 960
    float result = static_cast<float>(fixed_x) / scale; // Convert back

    std::cout << "Fixed: " << fixed_x << ", Floating: " << result << std::endl;
    return 0;
}
```

### ✅ Non-Power of 2 Scale (e.g., 3, 5, 7, ...)
- Use **normal multiplication and division** (`*` and `/`).
- Bitwise shifting does not work correctly.

#### Example (Non-Power of 2 Scale):
```cpp
#include <iostream>

int main() {
    float x = 3.75;
    int scale = 3; // Not a power of 2

    int fixed_x = static_cast<int>(x * scale); // 3.75 * 3 = 11
    float result = static_cast<float>(fixed_x) / scale; // Convert back

    std::cout << "Fixed: " << fixed_x << ", Floating: " << result << std::endl;
    return 0;
}
```

### 🔹 Rule of Thumb
- **If scale is a power of 2** → Use **bitwise shift**.
- **If scale is not a power of 2** → Use **normal arithmetic** (`*`, `/`).

# **WHY**
## Why Use Fixed-Point?
- **Performance**: Faster than floating-point operations, especially on systems without an FPU.
- **Precision Control**: Avoids some floating-point precision errors.

## Considerations
- **Overflow and Underflow**: Choose an appropriate scaling factor.
- **Precision Loss**: Limited by the number of bits allocated for the fractional part.

Fixed-point arithmetic is useful in embedded systems, game development, and other performance-critical applications.
