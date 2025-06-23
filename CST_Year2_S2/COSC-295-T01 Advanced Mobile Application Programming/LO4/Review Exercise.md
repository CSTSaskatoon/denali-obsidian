1. How would you call this function: `func myFunc(num: Int, num2: Int) -> Int`
`let myInt: Int = myFun(num: 1, num2: 2)`

2. Define a function called `doubleThem` with two params, the result will be the params added together and multiplied by 2. External names `number1` and `number2` and internal names `a` and `b`. The second param defaults to 0.
```swift
func doubleThem(number1 a: Int, number2 b: Int = 0) -> Int
{
	return (a + b)*2;
}
```

3. Define a function called `counter` which has 2 params which are a variadic parameter and a pass by reference parameter. Determine how many items are in the first parameter and set the second parameter to that
```swift
func counter(param1: Int..., param2: inout Int)
{
 param2 = param1.count; // param1 is an array
}
```

## Part 2
1. Will these work? Why or why not?
	1. `var f: (String)()` - idk
	2. `var myVar = Room(width: 1, length: 10)` - yes
	3. `var myInstance: Room?` - yes
	4. `public struct test { public var t1: Int = 1; public var t2: Int }` - yes
	5. `var test1: test = test();` - no, default constructor doesn't initialize all values
2. Add a count int property to Room, default to 0

```swift
func processIt(items: Int..., start: inout Int, process: (Int, Int) -> Int)
{
	for i in items
	{
		start = process(i, start)
	}
}
```

1. Add a method to increment count by 1
```swift
func incrementBy(i: Int, t: Int) -> Int
{
	return i + t;
}

func decrementBy(i: Int, t: Int) -> Int
{
	return t - i;
}

var result = 50;
// Some other shit
```

## Part 3
1. Define a protocol called `myProtocol` that has a method called `readInt` that returns an `Int` and a `computed Int` property called `lastInt` as `get` and `set`
2. Define a struct called `RGBColor` with 3 unsigned 8 bit integers - `Red`, `Green`, `Blue`
3. Define a class called `Crayon` with a property called `Color` of the type from Q2 and a `Double` `computed` property called `percentRemaining` which wraps a private property called `percentRem` which must be between 0 and 100

```swift
public protocol myProtocol
{
	func readInt() -> Int;
	var lastInt: Int { get; set; }
}
public struct RGBColor
{
	public var red: UInt8;
	public var green: UInt8;
	public var blue: UInt8;
}

public class Crayon
{
	public var Color: RGBColor = RGBColor(red: 0, green: 0, blue: 0);
	private var percentRem: Int = 100;
	public var percentRemaining: Int
	{
		get
		{
			return percentRem;
		}
		set
		{
			if newValue >= 0 && newValue <= 100
			{
				percentRem = newValue;
			}
		}
	}
}

```