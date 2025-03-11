Fixed-point arithmetic is a technique used to represent fractional numbers using integers and bitwise operations. It is commonly used in systems without floating-point units (FPUs) for better performance and precision control.

## How It Works

### 1. Conversion (Scaling Up)
- Choose a scaling factor, typically a power of 2 (e.g., `2^n`).
- Multiply the floating-point number by this factor to convert it into an integer.
- Use a left shift (`<<`) if the scaling factor is a power of 2.

#### Example:
```c
float x = 3.75;
int scale = 1 << 8; // 2^8 = 256
int fixed_x = (int)(x * scale); // 3.75 * 256 = 960
```

### 2. Perform Calculations
- Addition and subtraction work as usual.
- For multiplication, you may need to rescale after the operation.
- For division, scale properly to maintain precision.

#### Example:
```c
int fixed_y = (int)(2.5 * scale); // 2.5 * 256 = 640
int fixed_result = (fixed_x * fixed_y) / scale; // (960 * 640) / 256
```

### 3. Conversion Back (Scaling Down)
- Divide by the scaling factor to convert back to floating-point.
- Use a right shift (`>>`) if using a power of 2.

#### Example:
```c
float result = (float)fixed_result / scale; // Convert back to float
```

## Why Use Fixed-Point?
- **Performance**: Faster than floating-point operations, especially on systems without an FPU.
- **Precision Control**: Avoids some floating-point precision errors.

## Considerations
- **Overflow and Underflow**: Choose an appropriate scaling factor.
- **Precision Loss**: Limited by the number of bits allocated for the fractional part.

Fixed-point arithmetic is useful in embedded systems, game development, and other performance-critical applications.
