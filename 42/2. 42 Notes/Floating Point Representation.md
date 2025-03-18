## Components
A floating-point number is represented using:
- **Sign Bit (1 bit)**: Determines whether the number is positive (0) or negative (1).
- **Exponent (variable bits)**: Determines the scale of the number. More bits increase precision.
- **Mantissa (remaining bits)**: Represents the significant digits after the radix point.

## Example: Representing 5625
### **Implicit Normalization**
- Convert to scientific notation: 
  ```
  5.625 × 10^3
  ```
- **Exponent** = 3
- **Mantissa** = 625
- **Conversion Formula**:
  ```
  (-1)^S × 1.M × 2^(E - Bias)
  ```

### **Explicit Normalization**
- Convert to an alternate scientific notation:
  ```
  0.5625 × 10^4
  ```
- **Exponent** = 4
- **Mantissa** = 5625
- **Conversion Formula**:
  ```
  (-1)^S × 0.M × 2^(E - Bias)
  ```

## Finding the Bias (used for storing both -ve and +ve exponents)
If the exponent uses **N bits**, the bias is calculated as:
``` 
Bias = 2^(N-1) - 1
```

### Example: 4-bit Exponent
- Exponent range: 
  ```
  -8 to +7 (since 4 bits can store values from 0 to 15)
  ```
- Bias calculation:
  ```
  Bias = 2^(4-1) - 1 = 2^3 - 1 = 7
  ```
- If the exponent is **3**, store it as (MUST ADD THE BIAS FIRST):
  ```
  3 + 7 = 10 (Decimal) → 1010 (Binary)
  ```
  This binary representation is stored in the exponent bits.

## Converting 0.625 to Binary

### **Step 1: Multiply by 2 Repeatedly**
We repeatedly multiply the decimal fraction by 2, recording the **integer part** each time:

| Step | Decimal Value | × 2 | Integer Part | Fractional Part |
|------|--------------|----|--------------|----------------|
| 1    | 0.625       | 1.25 | **1**          | 0.25          |
| 2    | 0.25        | 0.50 | **0**          | 0.50          |
| 3    | 0.50        | 1.00 | **1**          | 0.00 (stops)  |

### **Step 2: Read the Integer Parts**
Reading from top to bottom, the binary representation is:

```
0.625₁₀ = 0.101₂
```

### **Verification**
Convert **0.101₂** back to decimal:

```
(1 × 2^(-1)) + (0 × 2^(-2)) + (1 × 2^(-3)) = 0.5 + 0 + 0.125 = 0.625
```


✅ The conversion is correct!

### **Steps**
- **0.625 (decimal) = 0.101 (binary)**
- Multiply by **2**, take integer parts, repeat until fraction = **0**
- Read the integer parts from **top to bottom**

## Summary
1. Convert the number into scientific notation.
2. Normalize it into implicit or explicit form.
3. Determine the exponent and mantissa.
4. Use the formula **Bias = 2^(N-1) - 1** to find the biased exponent.
5. Convert the exponent to binary and store it.
6. Use the conversion formula to retrieve the original value when needed.
