Abstract Classes Can't Be instantiated (Can't create an object of this, have to be more specific)
	Sometimes we want to define high-level characteristics, but only as a classification method
	Sometimes we want to delay the definition of certain methods until we get more info about the method.

Can be used as datatypes
An abstract class can have constructors (only able to be called from the subclass)
A class that contains abstract methods must be abstract, but you can make an abstract class with no abstract methods
An abstract method cannot be contained by a non-abstract class
In very unusual circumstances you can declare abstract sub classes of concrete (non-abstract) classes 

Abstract Classes Example (Monster)

Methods isDeadly and consumes are abstract

Monsters
	All speeds must be between 0 and 10
	Out of bounds range is given set the speed to 5
	Monsters are equal if they have the same name
	Compared by scare factor



//QUESTIONS
	If you have a method that is "required" in all of your sub classes of an abstract method, should it always be an abstract method in your superclass?
	In addition to this, what if that "required" method is a getter/setter method? Or should that variable just be set as protected instead?
	
