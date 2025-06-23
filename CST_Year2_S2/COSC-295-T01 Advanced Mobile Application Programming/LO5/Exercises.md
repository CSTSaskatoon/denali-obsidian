## Q1
Write an operator overloaded function to divide a Double by an Integer and return a Double and add another function to divide an integer by a double and return a double

```swift
func /(left: Double, right: Int) -> Double
{
	if right == 0
	{
		return 0.0
	}
	return left / Double(right)
}

func /(left: Int, right: Double) -> Double
{
	if right == 0.0
	{
		return 0.0
	}
	return Double(left) / right
}
```

## Q2
Store name, number of cats, and number of dogs in a Tuple. Create an array with a few entries in it. Then lop through the array and using a switch statement display one of the following messages - "Name likes cats better than dogs", "Name likes dogs better than cats", or "Name likes dogs and cats the same amount", or "Name does not like cats or dogs", or "Invalid values"

```swift
var people = [("Blazed", 4, 5), ("Spoonkid", 1, 3), ("Dave", 0, 0), ("luckyllama", -5, 4)]

for p in people
{
	switch(p)
	{
		case let (_, cats, dogs) where cats < 0 || dogs < 0: print("Invalid values")
		case let (name, cats, dogs) where p.cats > p.dogs: Print("\(name) likes cats better than dogs")
		case let (name, cats, dogs) where p.cats < p.dogs: Print("\(name) likes dogs better than cats")
		case let (name, cats, dogs) where p.cats == p.dogs: Print("\(name) likes cats and dogs the same amount")
		default: print("\(p.name) doesn't like cats or dogs")
	}
}
```