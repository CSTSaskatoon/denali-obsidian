Create an `Account` class
The `withdraw` method should only withdraw if there is enough money left in the account (Balance can't go below 0)
- Return true if the withdraw was successful and false otherwise

`Description` is a computed property - return a string containing `accountId has balance`

Create a `ChequingAccount` class that inherits from `Account` and has an attribute called `overdraftLimit`
- Should override the `withdraw` method to take overdraft limit into account
- override the `Description` property to include overdraft limit in string - `accountId has balance and an overdraft limit of overdraftLimit`

```swift
public class Account
{
	internal var accountId: String;
	internal var balance: Double;
	public var description: String { return "\(accountId) has $\(balance)" }
	public init(startingBalance: Double) { balance = startingBalance; accountId = Uuid.Generate(); }

	public withdraw(amount: Double) -> bool
	{
		if (amount < 0)
		{
			return false;
		}
		
		if (amount < balance)
		{
			balance -= amount;
			return true;
		}
		return false;
	}
}

public class ChequingAccount: Account
{
	internal var overdraftLimit: Double;
	public override var description: String { return "\(accountId) has $\(balance) and an overdraft limit of $\(overdraftLimit)" }
	public init(startingBalance: Double, overdraftLimit: Double)
	{
		self.overdraftLimit = overdraftLimit;
		super.init(startingBlance: startingBalance); // Have to call the super initializer last
	}

	public withdraw(amount: Double) -> bool
	{
		if (amount < 0)
		{
			return false;
		}
		if (amount < balance + overdraftLimit)
		{
			balance -= amount;
			return true;
		}
		return false;
	}
}
```