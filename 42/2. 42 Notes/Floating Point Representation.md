Represented with
Sign - 1 bit
Exponent - depends on how many bits you want to reserve, more bits will increase accuracy
Mantissa - all values after the radix point 

eg: if exponent is 8 bits
- represents values from 2^-8 - 2^8, but flip them and make them positive, 2^0 - 2^15
- hence, bias is 127
- 

eg: 5625

Implicit Normalization
5.625 * 10^3

Exponent = 3
Mantissa = 625

Explicit Normalization
0.5625 * 10^4

Exponent = 4
Mantissa = 5625

