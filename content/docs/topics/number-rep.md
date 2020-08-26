# Number Rep + Floating Point

Know how to convert between binary/hex/decimal. It's probably second nature by this point so we didn't include it.

![Unit conversions](/images/conversion.png)

## Negative Numbers?

1. Sign and Magnitude
	- One sign bit, rest same as unsigned
	- Ex: **0**0011 = +3, **1**0011 = -3
2. Biased Notation
	- Predetermined bias, applied to all numbers.
	- Ex: bias is -15. 00011 = 3-15 = -12
3. One's Complement
	- 00011 = +3 // Positive, same as usual
	- 11100 = -3 // Flip bits to get negative
4. Two's Complement
	- 00011 = +3 // Positive, same as unsigned
	- 11101 = -3 // Flip bits and add 1 to get negative version

![Number Rep Table](/images/reps.png)

## Floating Point

For standard (32-bit precision) floating point number: bias is **-127**. Add -127 to whatever the exponent is as an unsigned number.

![Floating Point Table](/images/floatingpoint.png)

Bias: 2^(# of exponent bits - 1) - 1

## Approach to Tricky Qs
{{< expand "What is the largest odd floating point number?">}}
same as _when does step size become greater than 1?_
{{< /expand >}}
{{< expand "What is the largest floating number that is a multiple of 4 but not a multiple of 8?">}}
same as _when does step size become greater than 4?_
{{< /expand >}}
{{< expand "What is the minimum integer not representable?">}}
The minimum integer not representable is 2^(mantissa + 1) + 1 (step sizes will start to be greater than 1 in the least significant mantissa bit)
{{< /expand >}}
{{< expand "How do I figure out step size?">}}
**Main idea: limited number of steps between exponents. i.e., there are only 4 (arbitrary number) steps available between getting from 2^1 to 2^2 // 2^2 to 2^3 // so on and so forth, so floats get less precise the higher up you go.**
- Multiply 2^(-mantissa)*2^(exp-bias) to find step size
- When moving by one step to the subsequent number, increment mantissa in the smallest place! Step size determined by exponent. 
{{< /expand >}}



