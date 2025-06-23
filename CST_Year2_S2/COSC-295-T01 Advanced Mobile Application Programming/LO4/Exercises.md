## Q1
1. Which will work, why/why not
	1. `var day: Weekday = Weekday(rawValue: 5)` - returns an optional so won't work
	2. `var numbers = [10, 20, 30]` - this is fine
	3. (Inside an enum) `mutating func prevDay() { self = Weekday(self.rawValue - 1)! }` - missing the `rawValue:` label
2. Write a function called `kickout` that will take in a class called `House` and decrease the occupant property by 1

```swift
public class House
{
	public var occupant: Int = 2;
}

public func kickout(house: House)
{
	house.occupant -= 1;
}
```

3. Same as above but struct called `HouseStruct`

```swift
public struct HouseStruct
{
	public var occupant: Int = 2;
}

public func kickoutStruct(house: inout HouseStruct)
{
	house.occupant -= 1;
}
```