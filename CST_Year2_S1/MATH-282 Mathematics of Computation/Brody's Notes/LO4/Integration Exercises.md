Copy print line from Mike's ACFunction.

Results from Integration Exercises:
- Calculated integrals should work as expected if functions are implemented correctly
- Number of rectangles = $2^{\text{number of loops}}$
- Increased precision means better answers but more loops/rectangles required
- 30 `maxLoops` calculates $2^{30}$ or approximately 1 billion rectangles, so 30, 35 or 40 `maxLoops` would be fine (slow down significantly after 30)
- With precision 0, it goes on indefinitely (until it reaches `maxLoops`)
- For 31 loops or more, we need a **long** data type for the number of rectangles used since it will exceed the values stored in an **int**.
- For `FunctionWeird`, it does not come up with the right answer - it stops after 2 loops and 4 rectangles with answer 32 instead of 29.87. This is because two successive estimates had the same value, which is how we are calculating error and when to stop.

To make the left rectangle rule more efficient, see notes (including implementation notes) in "Left Rectangle Rules Algorithm.docx". In particular:
- We are multiplying by the same width, so we have, for instance:
	$$f(3)*1.5 + f(4.5)*1.5 + f(6)*1.5 + f(7.5)*1.5$$
$$(f(3) + f(4.5) + f(6) + f(7.5))*1.5$$
	which saves us a lot of multiplications and is the same by the distributive law.
- Note that when we double the number of rectangles, we are re-using heights. For instance:
	When we move from:
$$(f(3) + f(6)) * 3\text { to }((f(3) + f(4.6) + f(6) + f(7.5)) * 1.5$$
	We see that only the odd-numbered heights are new; so if we just store the previous heights, we save a bunch of function calculations.
