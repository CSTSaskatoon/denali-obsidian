Iterative methods for repetitively calculating values.
### General algorithm for iterative method
- Start with an *initial approximation*
- While the approximation is not "*close enough*"
	- *Fine a better approximation*
- Return the last approximation

For any specific iterative method, we just need to figure out the parts shown in *italics*

Also, such methods only work if the approximations "converge" (get closer to the exact answer)
### Examples
Example 1: Exponential Function
Recall
$$e = 1/0! + 1/1! + 1/2! + ... = E^{∞}_{k=0} \frac 1 {k!}$$
![[Pasted image 20240911084834.png]]
This process can be extended to the exponential function, which is $e^x$ for some value $x$.
$$e^x = 1 + \frac x {1!} + \frac {x^2} {2!} + \frac {x^3} {3!} + \text{...}$$
$$E^∞_{k=0} \frac {x^k} {k!}$$
Initial approximation: 1
Better approximation: add the next term for $k$, $\frac {x^k} {k!}$
Close enough: Check the difference between successive calculations.
We started by calculating $e^x$ using calculations for $x^k$ and $k!$ separately, and then dividing them; but note that each term is related to the previous term, such that $\text {new term = old term} * \frac x k$

Also, we can note that the error $\text {new result - old result}$ is just value of the $\text {new term}$
Also, it is better to use relative error than just the amount of error so that we can better handle really big/really small numbers.

Finally, note that $e^{-x} = \frac 1 {e^x}$ so we can always calculate positive values of $x$
### Example 2: Sine Function
We can calculate the sine of an angle in $x$ in radians using the formula:
$$\sum ^∞ _{k=0} \frac {(-1)^k} {(2k + 1)!} x^{2k + 1} = x - \frac {x^3} {3!} + \frac {x^5} {5!} - \frac {x^7} {7!} + \text {...} = \text {sin } x$$
Note that x is in radians; what does that mean? Recall that a circle has 360 degrees. Another way to measure angles is to take the radius along the edge of the circle and see how many radiuses that angle would cut off along the circumference.
![[Pasted image 20240913090854.png]]
Note that 360 degrees is the whole circle, and radius goes around the whole circle $2 * pi$ times (since the circumference is $pi * diameter$, and diameter is $2*radius$).

So 360 degrees = $2*pi$ radians
180 degrees = $pi$ radians
90 degrees = $\frac {pi} 2$ radians

Going back to: $$\sum ^∞ _{k=0} \frac {(-1)^k} {(2k + 1)!} x^{2k + 1} = x - \frac {x^3} {3!} + \frac {x^5} {5!} - \frac {x^7} {7!} + \text {...} = \text {sin } x$$
We see that we have an initial approximation ($x$), we have a way of getting a better approximation (add a term), and a way of checking if we're close enough (check successive guesses).

We can improve our answer:
- First we can use the relationship between terms:
	Each term is $-1 * \text {previous term} * x * \frac x {(2k +1)}$
- Second we can just use the amount of the term to calculate error,
- Third we can take the angle and take the remainder of the number divided by $2 * pi$
### Example 3: Finding square roots
Given $x$ we seek $\sqrt x$ to some desired precision
We know that $\sqrt x$ is always between $1$ and $x$. This gives us upper and lower boundaries. We can guess halfway between the upper and lower boundaries and compare $\text {guess}^2$ to $x$.
- If $\text {guess}^2$ equals $x$, the $\text {guess}$ is the square root of $x$
- If $\text {guess}^2$ is greater than $x$, then $\text {guess}$ is too large and is a new upper boundary
- If $\text {guess}^2$ is less than $x$, then $\text {guess}$ is too small and is a new lower boundary

We can use the new boundaries to repeat this process until "close enough".
**PARTIAL algorithm for finding square roots by bisection**
- Given $x$, precision
- Guess <- 0
- If $x$ < 0
	- Indicate error
- Else if $x$ > 0
	- Lower <- 1
	- Upper <- $x$
	- KeepGoing <- True
	- While KeepGoing
		- Guess<- (Lower + Upper) / 2
		- Test <- guess * guess
		- If test equals $x$
			- KeepGoing <- False
		- else if test > $x$
			- Upper <- guess
		- else
			- Lower <- Guess
		- if (Upper - Lower) <= precision
			- KeepGoing <- False
- return guess

We can implement using doubles or BigDecimals (see OneDrive for examples).

**Square roots using the Babylonian method**
- Given $x$, we seek $a = \sqrt x$ to some disired precision
- Make an initial guess $a_0 = 1$
$$a_n = (a_{n-1} + \frac x {a_{n-1}} / 2)$$
New guess = $0.5 * \text{(oldGuess} + x /\text{oldGuess)}$
Creates $a_0$, $a_1$, $a_2$, $...$ -> $a$
**Algorithm for finding square roots by the Babylonian method**
- Given $x$, precision
- guess <- 0
- if x < 0
	- Indicate error
- else if x > 0
	- guess <- 1
	- keepGoing <- false
	- while keepGoing
		- oldGuess <- guess
		- guess <- (oldGuess + x / oldGuess) / 2
		- if (|(guess - oldGuess)/guess| <= precision)
			- keepGoing <- false
- return guess

Coding is left as an exercise for the students.
## Example 4: Finding the zeros (or roots) of a function (important)
>Function: a rule that maps values of $x$ to values of $f(x)$ 

How can we express functions?
1. Formula or equation
Examples:
$f(x) = 2x + 1$, or $y = 2x + 1$
$g(x) =  \text sin (x)$
$h(x) = e^x - \sqrt x$
$p(x) = x^2 - 2$ - Polynomial
2. We can show some function values in a table
Examples:

| $x$  | $f(x) = 2x + 1$ |
| ---- | --------------- |
| -1   | -1              |
| -0.5 | 0               |
| 0    | 1               |
| 0.5  | 2               |
| 1    | 3               |
3. We can show functions on a graph

A "*zero*" or "root" of a function is a value of $x$ where $f(x) = 0$.
- Note: not $f(0)$

We can find the zero of a function in several ways:
- If we're lucky, it may show up in the table of values, in the table over, you can see $-0.5 = 0$
- We can also find the zeros on a graph - a zero is where the function touches the x-axis
- In some cases, we can solve analytically
Example:
$f(x) = 2x + 1$
$0 = 2x + 1$
$-1 = 2x$
$-\frac 1 2 = x$
- We can also use computational methods to find the zero of a function, in particular we will look at bisection
### Another Example
$$f(x) = 3x^2 - x - 2$$
$$(3x+2) (x-1)$$
Quadratic equation:
$$x = \frac {-b ± \sqrt{b^2 - 4ac}} {2a}$$
$x = 1$: = $\frac {-b ± \sqrt{b^2 - 4ac}} {2a}$ - Copy his excel sheet lol
#### Polynomial functions
A polynomial function is a function that is made up of sums of power of $x$
$$p(x) = a_0 + a_1x + a_2x^2 + \text {...} + a_nx^n$$
- Notes that $a_0$ is just $a_0x^0$, and $a_1x$ is just $a_1x^1$

Examples:
$f(x) = 2x + 1 = 1 + 2x$              is a polynomial of degree 1
$f(x) = 3x^2 - x - 2$                     is a polynomial of degree of 2
$p(x) = 9.5x^7 + 3x^5 - 2.1x^2 - 7$  is a polynomial of degree 7
The *degree* of a polynomial function is its highest power of $x$.

For $p(x)$, there are **at most** $d$ zeros if $p(x)$ of a degree $d$.
We can solve analytically for polynomials of degree 1, 2, 3, and 4, but there is no general solution for finding zeros of higher degrees.
### Computational Approaches of Finding Zeros: Bisection
- Suppose we have $x_1$ where $f(x_1) > 0$ and $x_2$ where $f(x_2) < 0$. Then if the function is continuous (smoothly connected) in that range, $f(x)$ must have a zero between $x_1$ and $x_2$, since the function switches from positive to negative and must touch the x-axis.

To find the zero, we can use bisection
- Guess halfway between $x_1$ and $x_2$, so $\text guess = (x_1 + x_2) / 2$
- Calculate $f(\text guess)$
- if $f(\text guess)$ is 0, $\text guess$ is a zero of the function (not all)
- if $f(\text guess) >  0$, $\text guess$ is a new value for $x_1$
- if $f(\text guess) >  0$, $\text guess$ is a new value for $x_2$

Repeating the process until we are "close enough" (when the difference between $x_1$ and $x_2$ is small enough)
>See "Quadratic function.xlsx" and "Sample function for zero-finding by bisection.xlsx" and "function examples.xlsx" in the **LO2** folder of the OneDrive folder for examples
### Algorithm for zero-finding using Bisection
Given $f(x)$, xEvalPos, xEvalNeg, precision
keepGoing <- true
while (keepGoing)
	guess <- (xEvalPos + xEvalNeg) / 2
	fAtGuess <- f(guess)
	if fAtGuess equals 0
		keepGoing <- false
	else if fAtGuess > 0
		xEvalPos <- guess
	else
		xEvalNeg <- guess
	error <- |xEvalpos - xEvalNeg|
	if error <= precision
		keepGoing <- flase
return guess
>See also "Algorithm For Finding Zeros Using Bisection.docx" on the OneDrive folder in the **LO2** folder for the algorithm and more details.

To code in Java, we need classes to represent each function and way to store common code for every function.
>See the starting code in the **Function** folder on the OneDrive in the **LO2** folder
- **IFunction.java** is an interface or "contract" for what our function must implement - add the definition of the **findZero** method to it
- **ACFunction.java** is an abstract class for what ALL functions can do - implement the **findZero** method in it, using **this.calculate()** to get function values
- **Function1.java** and **Function2.java** extend the abstract class to implement a specific **calculate()** method
- **TestFunction.java** creates the function objects and calls the **printTable** and **findZero** methods to find the zero of the functions
## Aside
Search engine called *WolframAlpha* to quickly graph some functions and get solutions.
# New Functions
We can add new functions like:
$$f(x) = e^x - \cos x - 1$$
We do this by adding a new function class that extends `ACFunction`.

Note that bisection only works if we have positive and negative function values. If a function just touches the x-axis, we can NOT find such starting values to find that zero. Also, the function must be continuous (smoothly connected) between the starting values. Finally, we can only find one zero between the starting points if the function goes up and down and up and down, we will NOT find the other zero.

More info:
[Zero of a function - Wikipedia](https://en.wikipedia.org/wiki/Zero_of_a_function) and [Root-finding algorithm - Wikipedia](https://en.wikipedia.org/wiki/Root-finding_algorithm)
