Represented with
Sign - 1 bit
Exponent - depends on how many bits you want to reserve, more bits will increase accuracy
Mantissa - all values after the radix point 

eg: 5625

Implicit Normalization
5.625 * 10^3

Exponent = 3
Mantissa = 625

Explicit Normalization
0.5625 * 10^4

Exponent = 4
Mantissa = 5625

eg: if exponent is 4 bits
- represents values from 2^-8 - 2^8, but flip them and make them positive, 2^0 - 2^15
- hence, bias is 127
- How to use it:
	- if found that exponent is 3, 2^3 = 8, convert to binary to store in the 4 bits space