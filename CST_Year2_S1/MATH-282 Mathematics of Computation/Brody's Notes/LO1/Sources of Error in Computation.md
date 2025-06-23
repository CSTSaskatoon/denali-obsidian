### Number Systems
Set of values and operators.

Examples:
1. Boolean values: {true, false} with operators AND, OR, NOT, etc.
   Represented by 1, and 0; operators result in other Boolean values; no error introduced.
2. Integers:
   Natural numbers: {1, 2, 3, ...}
   Whole numbers: {0, 1, 2, 3, ...}
   Integers: {..., -3, -2, -1, 0, 1, 2, 3, ...} with operators +, -, \*, /, %
   
Java uses **Byte, short, int, long** - limited by number of bits.
Operators can introduce errors - example * for factorials - leads to overflow.

How can we deal with errors? Use more bits; use classes like `BigInteger` in Java.
Drawback - more bits can lead to performance issues.

Also, what do we do with division?
int: 7 / 2 = 3 (remainder 1)
double: 7.0 / 2.0 = 3.5 (non-integer)

3. Real:
![[Pasted image 20240830091809.png]]
With operators +, -,  \*, /, square root

Java uses **double, float** - floating-point numbers - similar to *scientific notation*.

Example:
12! = $4.790016 * 10^8 = 4.790016E8$
A certain number of digits are used for the *mantissa* and the **exponent**.

Issues:
a. Overflow - numbers are too big for the bits in the exponent (stored as "infinity").

b. Underflow - numbers where the negative exponent is too big (stored as 0).

c. *Precision* - mantissa can't be stored in the bits assigned.

d. Representation - numbers can't be represented (in the number systems we have) - 
example: 1 / 3 in decimal is 0.333... (mantissa rounds off results).
Computers use binary, which has more problems - for instance, one tenth = 0.1 (decimal, which is exact) but equals 0.000110011001100...(base 2)

e. Calculations with operators can introduce problems with underflow and overflow, but also with precision (even with exact values in base 10).
### How do we deal with error in real numbers
- We can round off (controller error)
- We can introduce more digits (still limited by representation)
- We can switch from binary to decimal (for instance, the `BigDecimal` class from Java) - can introduce performance issues

Example (*might see something like this on the exam*): Suppose you are working with a decimal machine (rather than binary) that stores numbers in the form `±#.### * 10^±##`. Assume calculations can be done with exact precision, but results of any calculation must be rounded off to be stored as shown above after **every** calculation step.
- Largest possible: `9.999 * 10^99`
- The smallest possible positive number: `0.001 * 10^-99` or `1.000 * 10^-99` depending on how you represent the decimal point number (i.e. having 0 or 1 at the start).
- 5387 would be represented as `5.387 * 10^03` (stored as `538703` since the computer already knows to represent numbers in this way. There is also no error in this representation).
- 1.236 would be represented as `1.236 * 10^00` - no error.
- -0.012343 would be represented as `-1.234 * 10^-2` - precision error
- $5387 + 1.236 = 5388.236 = 5.388 * 10^{03}$ - error introduced
- $5387 * 1.236 = 6658.332 = 6.658 * 10^{03}$ - error introduced
## Types of Error in Computation
1. Representation error (due to limited precision)
2. Measurement error (from humans/equipment)
3. Round-off error (from computer representation, measurement, or calculations) - can sometimes be quantified - for example: `24 ± 0.5 kg`
4. Truncation error - for formulas with many/infinite terms, if we only add some of those terms.
   For instance, e = 1/0! = 1/1! + 1/2! + ... = $$\sum ^∞ _{n=0} \frac 1 {n!} = e$$We introduce truncation error when calculating e since we can't add infinitely many terms. Note that order of calculations matters.

Intro truncations error when calculating e

Examples: Suppose we are working with the machine described earlier:
$$3877 = 3.877 * 10^3$$
$$1.2 = 1.200 * 10^0$$
$$0.4 = 4.000 * 10^-1$$
$$0.3 = 3.000 * 10^-1$$
Added up in order:
`3877 + 1.3 = 3878.2 represented as 3,878 * 10^3 = 3878 (some roundoff error)`
`3878 + 0.4 = 3878.4 represented as 3.878 * 10^3 = 3878 + 0.3 = 3878.3 reporesented as 3.878 * 10^3 (some round off error)`
`3878 + 0.3 = 3878.3 represented as 3.878 * 10^3 = 3878 (some round off error)`
Add up in reverse order:
`0.3 + 0.4 = 0.7 represented as 7.000 * 10^-1 (no error)`
`0.7 + 1.2 = 1.9 represented as 1.900 * 10^0 (no error)`
`1.9 + 3877 = 3878.9 represented as 3.879 * 10^3 = 3879 (some reoundoff error)`
Correct answer (mathematically) could be `3878.9`

So it is NOT true for this computer that (a + b) + c = a + (b + c) \[Associative property]
### So why don't we always worry about error?
Usually, we don't need complete precision.
We can usually get more precision.
Round error may cancel.
Example: poll results
`10 says bowl   10/30 = 33% (roundoff error)
`20 say cone    20/30 = 67% (roundoff error)
`30 total       33% + 36% = 100% (no error - same as 30/30)`

Why should we worry?
**Awareness**
For instance, don't expect doubles to be exactly equal; for reporting - for instance, `17C = 62.6F` but `17` probably wasn't an exact value; report as `63F`.
- Extra precision can be performance - intensive
- Roundoff errors may accumulate

Example: poll results
`10 say chocolate    10/30 = 33% (some error)`
`10 say strawberry   10/30 = 33% (some error)`
`10 say vanilla      10/30 = 33% (some error)`
`30 total            33% + 33% + 33% = 99% (error has grown)`
## Calculating errors in computation
Suppose we have:
- Exact value $x$
- Approximated by $x_a$
- With error $E_x$

Then
$\text {Exact}$ = approximate + error:$$x = x_a + E_x$$
$\text {Error}$ = exact - approximate:$$E_x = x - x_a \text { (may be positive or negative)}$$
$\text {Size}$ of the is the absolute error:$$|E_x| \text{ (removes any negative sign)}$$
$\text {Relative Error}$ = error / exact:$$E_x / x ≈ E_x / x_a$$
Same thing but with properly showing symbols:
![[Pasted image 20240906082919.png]]

Example 1:
Suppose $x = 15.2$ and $x_a = 15$; then $E_x = 15.2 -15 = 0.2$
- The absolute error $|E_x|$ would be $0.2$ as well
- The relative error would be $0.2 / 15.2 = 0.013$ or 1.3%

Suppose $y = 399.8$ and $y_a = 400$; then $E_y = 39.8 - 400 = -0.2$
- The absolute error `|Ey|` would be `|-0.2| = 0.2`
- The relative error would be `0.2 / 399.8 = -0.0005` or `-0.05%`

Example 2:
Suppose `x = 123 +- 0.5`; then `Xa = 123` and `Ex = +-0.5` (at maximum)
- Then absolute (maximum) error would be `0.5`
- Relative error would be `±0.5 / 123 = +-0.004` or `±0.4%` (max)
### Addition
Suppose we have `X = Xa + Ex` and `Y = Ya + Ey`
`X + Y = (Xa + Ex) + (Ya + Ey)`
`      = Xa + Ya + Ex + Ey`
Exact = approximation + error
`Ex+y = Ex + Ey`
Note that errors may be positive or negative, so error may grown or cancel.
Relative error = error / exact = `(Ex + Ey) / X + Y`
Assume for now that `X` and `Y` are positive. Then the top part of the equation could grow, but the bottom part of the equation `(X + Y)` will grow. So relative error will be somewhat stable.

Example 1:
- Suppose `X = 204` and `Xa = 200`, so `Ex = 4` and rel. error = `0.0196 = 1.96%`
- Suppose `Y = 123` and `Ya = 120` so `Ey = 3` and rel. error = `3 / 123 = 0.0244 = 2.44%`
- Then `X + Y = 327` (exactly), but the best approximation would be `Xa + Ya = 200 + 120 = 320`
- Error would be `Ex+y = Ex + Ey` = `4 + 3 = 7` or `327 - 320 = 7`
- Relative error = error / exact = `7 / 327 = 0/0214 = 2.14%` (which is between the relative error in `X` and in `Y`) This is a weighted average.

Example 2:
- Suppose x = 200 ± 10
$x_a$ = 200, $E_x$ = ±10 (at max), rel. error = ±10 / 200 = ±0.05 = ±5%
- Suppose y = 160 ± 4
$y_a$ = 160, $E_y$ = ±4 (at max), rel. error = ±4 / 160 = ±0.025 = ±2.5%
Then $x$ + $y$ = $x_a$ + $y_a$ = 200 + 160 = 360
Error would be $E_{x+y}$ = $E_x$ + $E_y$ = (±10) + (±4) = ±14 (at maximum)
Rel. error = error / exact = ±14 / 360 = ±0.0389 = ±3.89% (which is between 2.5% and 5%)

Note that this can also be expressed as follows:
x = 200 ± 10 = 190...210 as a range of values
y = 160 ± 4 =   156...164
x + y                 346...374 which is 360 ± 14
### Subtraction
- Suppose we have $x$ = $x_a$ + $E_x$ and $y_a$ = $y_a$ + $E_y$ (with x and y positive)
x - y = ($x_a$ + $E_x$) - ($y_a$ + $E_y$)
x - y = $x_a$ - $y_a$ + $E_x$ - $E_y$
Exact = approx. + error
$E_{x-y}$ = $E_x$ - $E_y$ (but recall each error could be positive or negative, so the error may grow)
Relative error = ($E_x$ - $E_y$) / (x - y)
Value on top may grow, but value on bottom will be less than at least one of x or y, so relative error in subtraction may grow quickly.

Example 1:

|       | Exacy | Approx | Error | Relative |                                            |
| ----- | ----- | ------ | ----- | -------- | ------------------------------------------ |
| x     | 103   | 100    | 3     | 2.9%     |                                            |
| y     | 62    | 60     | 2     | 3.2%     |                                            |
| x - y | 41    | 40     | 1     | 2.4%     | Error cancels out - relative error shrinks |
Example 2:

|       | Exacy | Approx | Error | Relative |                                              |
| ----- | ----- | ------ | ----- | -------- | -------------------------------------------- |
| x     | 103   | 100    | 3     | 2.9%     |                                              |
| y     | 82    | 80     | 2     | 2.4%     |                                              |
| x - y | 21    | 20     | 1     | 4.8%     | Error cancels out, but relative errors grows |
Example 3:

|       | Exacy | Approx | Error | Relative |                                                  |
| ----- | ----- | ------ | ----- | -------- | ------------------------------------------------ |
| x     | 103   | 100    | 3     | 2.9%     |                                                  |
| y     | 58    | 60     | -2    | -3.4%    |                                                  |
| x - y | 45    | 40     | 5     | 11.1%    | Error does not cancel - rec. error grows quickly |
Example 4:
- Suppose x = 200 ± 10
$x_a$ = 200, $E_x$ = ±10 (at max), relative error = ±10 / 200 = ±0.05 = ±5%

- Suppose y = 160 ± 4
$y_a$ = 160, $E_y$ = ±4 (at max), rel. error = ±4 / 160 = ±0.025 = ±2.5%
x - y = 200 - 160 = 40
$E_{x-y}$ = $E_x$ - $E_y$ = (±10) - (±4) = \[±6 NO! wrong] = ±14 (at max)
>Always add the errors together positively
- Rel. error = error / exact = ±14 / 40 = ±0.35 = ±35%
or
x = 200 ± 10 = 190...210 but could be   190...210 (small to large)
y = 160 ± 4 =   156...164 but could be   164...156 (large to small, look at this when subtracting)
x +-y                 ~~34...46~~     so at max        26...54 = 40 ±14
### Multiplication
- Suppose we have $x$ = $x_a$ + $E_x$ and $y_a$ = $y_a$ + $E_y$ (with x and y positive)
Then:
$xy$ = $(x_a + E_x) * (y_a + E_y)$, multiplication of terms distributed using FOIL
$xy$ = $x_ay_a + x_aE_y + E_xy_a + E_xE_y$
Exact = approx. + error
So $E_{xy}$ = $x_aE_y + E_xy_a + E_xE_y$
Relative error= error / exact = $(x_aE_y + E_xy_a + E_xE_y) / xy$
![[Pasted image 20240906094648.png]]
Rel. error = $$x_aE_y+y_aE_x+E_xE_y / xy ≈ x_aE_y+y_aE_x / x_ay_a = (*x_a*E_y / x_ay_a) + (y_aE_x / x_ay_a)$$$$ ≈ \text { rel. error in } y + \text { rel. error in }x$$
So relative error may in a stable fashion.

Example 1:

|     | Exact | Approx | Error | Relative |
| --- | ----- | ------ | ----- | -------- |
| x   | 103   | 100    | 3     | 2.9%     |
| y   | 62    | 60     | 2     | 3.2%     |
| xy  | 6386  | 6000   | 386   | 6.0%     |
|     |       |        | 386   | 6.1%     |
Example 2:

|     | Exact | Approx | Error | Relative |
| --- | ----- | ------ | ----- | -------- |
| x   | 103   | 100    | 3     | 2.9%     |
| y   | 58    | 60     | -2    | -3.4%    |
| xy  | 5974  | 6000   | -26   | -0.4%    |
|     |       |        | -26   | -0.5%    |
Example 3:
- Suppose $x$ = 200 ± 10
	$x_a$ = 200, $E_x$ = (at max), rel. error = ±10 / 200 = ±5%
- Suppose $y$ = 100 ± 4
	$y_a$ = 160, $E_y$ = ±4 (at max), rel. error = ±4 / 160 = ±2.5%
	$xy$ = 200 * 160 = 32,000
	$E_{xy}$ = $x_a$$E_y$ + $E_x$$y_a$ + $E_x$$E_y$ = 200 * (±4) + 160 * (±10) + (±4) * (±10)
	= (±800) + (±1600) + (±40) = ±2440
	Relative error = error / exact ~= error / approx. = ±2440 / 32,000
	= ±0.07625 = ±7.6%
	Or
	rel. error ~= rel. error in $x$ + rel. error in $y$ = (±5%) + (±2.5%) = ±7.5%
- Or
	$x$ = 200 ± 10    190...210
	$y$ = 160 ± 4      156...164
	$xy$                      29,640...34,440 or roughly 32,000 ± 2440
### Division
Same as multiplications, rel. error $x$ + rel. error in $y$ similar to multiplication.