Objects are the first thing that is no longer the basics of programming

Not allowed to use Java.Utils.Arrays on the midterm

Objects and Object-Oriented Programming

Movivations
	We can solve many basic programming problems using selections, loops, arrays and methods. However, these don't scale well for GUIs and large scale software systems

Objectives
	Describe objects and classes
	Demonstrate how to define and create objects
	Demonstrate how to secure data and methods
	Distinguish between instance and static variables and methods
	work with objects in methods and arrays
	Create immutable objects from immutable classes to protect the content of objects

OO Programming concepts
	Object-oriented programming (OOP) involves programming using objects
	An object represents an entity in the real world that can be distinctively identified
	In Large systems, we typically are managing data regarding particular entities (Objects)
	Once we identify objects, we need to define them
	an object has a state and behavior
		State of an object consists of data fields(Properties) with their current values
		The behavior is defined by a set of methods
	We still need a way to define objects in code

Classes
	Classes are used to define objects of the same type
	uses variables to define state as data fields and methods to define behaviors
	a class provides a special type of method called a constructor which initiates objects from the class
	Data fields - Your data

Instances
	Instances are objects that you get from another class file, ex. the Scanner java object which you call and then you can have a data field that is whatever the user inputs
	You can leave instance variables blank, or initialize them.

Constructors
	Constructors can take in values (such as an int or String very similarily to how a method would)
	Same name as the class itself
	Do not have a return type (not even void)
	invoked using the new operator when an object is created. Initiates objects
	a constructor with no parameters is referred to as a no-arg constructor
	Syntax - new ClassName();
	simply putting the default of a variable into a Constructor instead of the base of the Class is not enough to prevent the method calling it from changing the value
		Ex - changing the radius of the circle from the Circle class. You can still do this even though the radius is inside of a Constructor

Class Abstraction and encapsulation
	When you are calling a class, you don't want to have to look at all the code in the class to be able to use it
	use class abstraction to seperate the class implementation from the use of the class.

Method Header 
	public int calculateArea(int length, int width);
		public - access modifier
		int - return value
		calculateArea - Method name
		(int length, int width) - parameters

Public Vs Private
	Methods are Public by default
	Variables are private by default

Access Modifiers and Accessor/Mutator Methods
	



