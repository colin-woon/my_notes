Represented with
Sign - 1 bit (+ve 0, -ve 1)
Exponent - depends on how many bits you want to reserve, more bits will increase accuracy
Mantissa - all values after the radix point 

eg: 5625

Implicit Normalization
5.625 * 10^3

Exponent = 3
Mantissa = 625

To convert it back to original value: (-1)^S * 1.M x 2^E-Bias

Explicit Normalization
0.5625 * 10^4

Exponent = 4
Mantissa = 5625

To convert it back to original value: (-1)^S * 0.M x 2^E-Bias

eg: if exponent is 4 bits
- represents exponent from -8 to +8, representing 0-15 in decimal, must be converted to binary
- hence, bias is 
- How to use it:
	- if found that exponent is 3, it should be 11 accordingly, then 11 is converted to binary and stored in the exponent bits

