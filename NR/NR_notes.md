# Numerical Recipes in C++
Notes on textbook "Numerical Recipes, The Art of Scientific Computing"
## Chapter 1 - Prelimineries
### Error, Accuracy and Stability
#### Floating point representation
S x M x b<sup>E-e</sub>
- S : sign
|:-:	|:-:	|
|  S	| sign 	|
|  E	| Exact integer exponent 	|
|  B	| Exact binary mantissa 	|
|  e	| Exponent bias 	|
32-bit floats:
- exponent: 8 bits
- exponent bias: 127
- mantissa: 23 bits
64-bit floats:
- exponent: 11 bits
- exponent bias: 1023
- mantissa: 52 bits
Left shifting mantissa as much as possible, and decrementing exponent accordingly -> normalized float
#### Roundoff error
Float addition:
- right shift mantissa of smaller-magnitude float while increasing its exponent by one until exponents match, add mantissas.
- least signifcant bits lost
- if magnitudes are very different, can be right shifted into oblivion
Accuracy of floating point numbers:
floats -  1.19 x 10<sup>-7</sup>
doubles - 2.22 x 10<sup>-16</sup>
C++: `numeric _limits <double>::epsilon()`
#### Truncation error:
When algorithm uses discrete approximation of discrete number of points:
- sum of values for integral
- sum of sequence of terms to approximate value
The difference between approxiximate values and true value is called the _truncation error_
Exists even on theoretical infinite precision floats
Under programmers control
#### Stability
Any roundoff error mixed into calculation at early stage has large effect on future computations
### Coding style
"Write code that is slightly less tricky than you are willing to read, but only slightly"
#### Bit-twiddling hacks:

|:-:	|:-:	|
|  `(v&(v-1))==0`	| True if v is power of 2 or zero 	|
|  `v&&((v&(v-1))==0)`	| True of v is power of 2 	|
|  `for (c=0;v;c++) v &= v - 1;`	| c is set to number of on bits in v 	|
|  e	| Exponent bias 	|
### Vectors
STL vectors are general purpose, and so can be slow for numerical computing
### Etc.
#### NaNs
Can define a NaN using:
- `static const Doub NaN = numeric_limits<Doub>::quiet_NaN();`
- `Uint proto_nan[2]=0xffffffff, 0x7fffffff; double NaN = *( double* )proto_nan;`
- `Doub NaN = sqrt(-1.);`
_quiet nan_ do not signal an exception, instead can continue to be used for calcualtions
_signalling nan_ used to signal an issues, like and invalid operation (square of negative number, pow(0, 0))
