$$\text area = \sum f(x) (x_2 - x_1)$$
$$\text area = \int f(x) * \Delta x$$
We are sometimes interesting in the area under the curve of a function (for instance, distance under a speed function). This is called the *integral* of the function.
To estimate the area, we can break it up into a bunch of rectangles. Adding up their area we get:
$$\text {Estimate of area} = \sum \text height * \text width = \sum f(x) \Delta x$$
Where $\Delta x = x_2 - x_1$ is the width of the rectangles.

More smaller rectangles give us a better result. AN "infinite" number of infinitely small rectangles will give up an exact answer - the integral of the function. The notation for that is:
$$\text Area = \int f(x) \Delta x$$
This can be solved mathematically for some functions but not all. For other functions, a computational approach is needed.
For our speed function $f(x) = \frac 1 4 x$, by the magic of calculus:
$$\int f(x) \Delta x = \int (\frac 1 4 x)\Delta x = \frac 1 8 x^2 = F(x)$$
This is called an "*indefinite integral*" because it doesn't go between any specific two values.

For the distance travelled from minutes 0 to 8, we have a "*definite integral*":
$$\int ^8 _0 f(x)\Delta x = \int ^8 _0 (\frac 1 4 x) \Delta x = F(8) - F(0) = \frac 1 8 (8)^2 - \frac 1 8 (0)^2 = 8$$
For minutes 6 to 8:
$$\int ^8 _6 f(x)\Delta x = \int ^8 _6 (\frac 1 4 x) \Delta x = F(8) - F(6) = \frac 1 8 (8)^2 - \frac 1 8 (6)^2 = 3.5$$

See "IntegrationBackfound MATH 280CST.docx" in the **LO4** folder in the OneDrive.

We are interested in computational approach that will take the area, device it into smaller pieces, and add up the area of the smaller pieces.
### Left Rectangle Rule
1. Take the integral being integrated and divide it into equal parts. So for:
$$\int ^9 _3 (\frac 1 3 x^2 - \frac 1 {300} x ^4) \Delta x$$
a. For 1 part, it would go from 3 to 9 for a width of 6.
b. For 2 parts, it would go from 3 to 6 and 6 to 9 for a width of 3.
c. For 4 parts, it would go from 3 to 4.5, 4.5 to 6, 6 to 7.5, and 7.5 to 9.
d. and so on...

2. For each part, create a rectangle with the height based on the value of $f(x)$ at the **left** edge.
a. For 1 part, use a height of $f(3)$
b. For 2 parts, use height of $f(3)$ and $f(6)$
c. For 4 parts, use height of $f(3)$, $f(4.5)$, $f(6)$, and $f(7.5)$
d. and so on...

3. Add up the area of the parts.
4. As long as estimate isn't "close enough", use more (twice as many) rectangles and continue.
#### Example
$$f(x) = \frac 1 3 x^2 - \frac 1 {300} x^4$$
Graph this and take table from $x$ values 0-10.
Follow "Sample function for inegration.xlsx" sheet in **LO4** folder that shows each rectangles estimates.
### Straightforward (but inefficient) algorithm
Given $f(x)$, left, right, precision, `maxLoops`
```
numRectangels <- 1
totalWidth <- right - left
height <- f(left)
estimate <- height * totalWidth*

numLoops <- 0
keepGoing <- true

while (keepGoing)
	add 1 to numLoops
	oldEstimate <- estimtate

	Multiply numRectangles by 2
	currentWidth <- totalWidth / numRectangles
	estimate <- 0

	for each rectanlge i starting at i =0
		currentLeft <- left + i * currentWidth
		currentHeight <- f(currentLeft)
		currentArea <- currentHeight * currentWidth
		Add currentArea to estimate

	error <- |estimate - oldEstimate|
	relError <- |error / estimate|
	
	if relError <= precision
		keepGoing = false
	else if numLoops >= maxLoops
		indicate problem
		keepGoing <- false

return estimate
```
### Trapezoid Rule
See "RectRuleExercise MATH282-CST.docs" Example from **LO4**.

Trapezoid rule says to divide the area into multiple trapezoid and add up their areas. Otherwise, it is the same as the rectangle rule.

See more of Michaels OneDrive files.
### Simpson's Rule
$$\text {Area } = \frac 1 6 (f(\text {left}) + 4 f(right))\text {width}$$
$$a$$
To review the previous integration processes and look forward to Simpson's Rule. Do the exercise "Shapes for integrals".

---
## Summary of rules:


| Left Rectangle Rule                                                 | Trapezoid Rule                                                             | Simpson's Rule                                                          |
| ------------------------------------------------------------------- | -------------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| One point (at left edge)                                            | Two points (at left and right edge)                                        | Three points in each interval (left, right, and the middle)             |
| Created rectangles (flat)<br>Degree 0 polynomial for each rectangle | Created trapezoids (line on top)<br>Degree 1 polynomial for each trapezoid | Created parabolas (curved on top)<br>Degree 2 polynomial for each point |

| Left Rectangle Rule                                              | Trapezoid Rule                                                                                            |
| ---------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| $\text {height}*\text {width} = f(\text {left}) * \text {width}$ | $\frac 1 2 * (h1 + h2) * \text {width} = \frac 1 2 * (f(\text {left} + f(\text {right})) * \text {width}$ |
|                                                                  | Exact answers for functions of straight lines (like $f(x) = \frac 1 4x)$)                                 |

Simpson's Rule
$$\frac 1 6 * (h_{left} + 4 * h_{middle} + h_{right} = f(\text {right} + 4f(\text {middle}) + f(\text {right}))/6*\text {width}$$
The algorithm for Simpson's rule is the same as the rectangle/trapezoid rule, except the we use the area formula for a second-degree polynomial instead of the area formula for the rectangle/trapezoid, which means that we also need the function value at $f(\text {middle})$.

Implementation of Simpson's rule is left for the students and will be required on *Assignment 2*.