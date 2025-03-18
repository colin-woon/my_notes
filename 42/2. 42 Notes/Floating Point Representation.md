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

## Finding the Bias
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
- If the exponent is **3**, store it as:
  ```
  3 + 7 = 10 (Decimal) → 1010 (Binary)
  ```
  This binary representation is stored in the exponent bits.

## Summary
1. Convert the number into scientific notation.
2. Normalize it into implicit or explicit form.
3. Determine the exponent and mantissa.
4. Use the formula **Bias = 2^(N-1) - 1** to find the biased exponent.
5. Convert the exponent to binary and store it.
6. Use the conversion formula to retrieve the original value when needed.
