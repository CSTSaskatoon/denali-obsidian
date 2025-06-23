# Structures in C (`struct`)
- A user-defined data type
- Allows data of different types to be combined in a single entity
- Somewhat like an array, but an array holds data of similar types only
- Can store data of any type
- defined using the keyword `struct`
- Also known as records
- Similar to classes in languages like Java and C#
- **Do not contain methods** (They do in `C++`)
- Can contain attributes such as primitive types, pointers, arrays, function pointers, and other structs
- **No inheritance or polymorphism**

## Syntax
- `struct` keyword used to define a struct
- `struct` defines a new data type that is a collection of primitive and user-defined data types

Basic syntax is
```c
struct [structure_tag] // "name" of the type of structure (like class name)
{
	// member variable 1 // Variable representing a primitive, array, pointer, function pointer, or another struct
	// member variable 2 // No limit on the number of member variables, similar idea to attributes in objects,
						 // but no access modifiers (Ex. public, private)
	// etc.
} [structure_variables]; // Rarely used, but if only a few instances are required the instance variables can be declared here

// Example - We want to track information regarding somebody's birthday
struct BirthDate
{
	// Attributes
	char name[NAME_SIZE];
	char gender;
	int day;
	int month;
	int year;
} Blazed, Spoonkid; // Valid syntax, but is rarely used

// Declaring the struct
struct BirthDate luckyllama;

// As a parameter to a function
void displayBirthDate(struct BirthDate bd);
```

## Using typedef to define a struct
- In both examples above, putting the keyword `struct` is required prior to the `struct`'s type
- Putting the keyword in front of every declaration becomes tedious
- Note that default values can be assigned using an initialization list, similar to an array.
- Struct is basically like an array except that every member is possibly a different data type

```c
typedef struct
{
	char name[NAME_SIZE];
	char gender;
	int day;
	int month;
	int year;
} BirthDateTD;

// Now it can be used like (note the absence of struct keyword)
BirthDateTD blazed = { "blazed", 'm', 1, 1, 1910 };

// As a parameter to a function
void displayBirthDate(BirthDateTD bd);
```

### Dynamically allocated
- All the structs declared so far are declared on the stack. Often, we will need dynamically allocated structs
- They can be dynamically allocated with `malloc`

```c
BirthDateTD* bdPtr = NULL; // Declare the pointer
bdPtr = (BirthDateTD*)malloc(sizeof(BirthDateTD)); // Allocate the memory, Cast is not required
```

## Accessing Attributes
- Method used to access attributes depends on the type of reference you have to access the struct

### `struct` reference
- Given a struct that is not a pointer, use dot syntax

```c
BirthDateTD bd1;

bd1.day = 10;
```

### Pointer to a `struct`
- Pointer must be dereferenced first, and then the attribute can be accessed.
- This is a *clumsy* way of accessing the attribute as we need to dereference in parenthesis and then use the dot operator

```c
BirthDateTD* bdPtr = NULL;
bdPtr = (BirthDateTD*)malloc(sizeof(BirthDateTD));

(*bdPtr).day = 31; // de-reference first
```

#### Arrow Operator
```c
bdPtr->day = 31; // Not sure if you are able to put spaces or not
```

## Struct and Union Review (Exercise)
1. Create a struct representing a computer containing space for a 9-computer ID (`string`), an `int` for the size of RAM, a `char` for a unit of RAM (like `M` for megabyte or `G` for gigabyte), and a pointer to dynamically allocated memory for a computer description
2. Assume you're working on an `x86` system where pointers are 4 bytes. How big would this struct be (Assume default 4-byte alignment)
3. What would the size be if the struct was contained in `#pragma pack(1)`?
4. Create a function that will take passed-in values and assign them to a struct to be returned. Show how it would be called.
5. Create a function that will take passed-in values and assign them to a dynamically allocated struct. Show how it would be called.
6. How would you define a union that would contain options for memory to be stored in bytes (as a `long long int`), in MB (as an `int`), in GB (as a `short`) or in TB (as a `char`)?
7. What would the size of the union be?
8. Is this valid code? Will the printout make sense?

```
// Didn't have time to copy the code
```

### Answers
#### 1
```c
typedef struct {
	char id[10]; // 9 characters + null terminator
	int ramSize;
	char ramUnit;
	char* descriptionPtr;
} Computer;
```

#### 2
- 10 + 2 bytes for `id` (line up on boundary)
- 4 bytes for `ramSize`
- 1 + 3 bytes for `ramUnit`
- 4 bytes for `descriptionPtr`
- 24 bytes total
- *Note the size depends on the order of the struct members, so if you put `ramUnit` after `id` you would save 4 bytes.*

#### 3
- 19 bytes
- *True regardless of order of member order because they are lining up on 1-byte boundaries*

#### 4
```c
Computer assignValues(char* id, int ram, char ramUnit, char* descriptionPtr)
{
	Computer retVal;
	strcpy(retVal.id, id);
	retVal.ramSize = ram;
	retVal.ramUnit = ramUnit;
	retVal.descriptionPtr = malloc(strlen(descriptionPtr) + 1);
	strcpy(retVal.descriptionPtr, descriptionPtr);
	return retVal;
}

Computer myComputer = assignValues("A12345678", 64, 'K', "Comodore 64");
// Do whatever you want
free(myComputer.descriptionPtr);
```

#### 5
```c
Computer* assignDynamic(char* id, int ram, char ramUnit, char* descriptionPtr)
{
	Computer retPtr = malloc(sizeof(Computer));
	strcpy(retPtr->id, id);
	retPtr->ramSize = ram;
	retPtr->ramUnit = ramUnit;
	retPtr->descriptionPtr = malloc(strlen(descriptionPtr) + 1);
	strcpy(Ptr->descriptionPtr, descriptionPtr);
	return retVal;
}

Computer* myComputerPtr = assignDynamic("A12345678", 64, 'K', "Comodore 64");
// Do whatever you want
free(myComputerPtr->descriptionPtr);
free(myComputerPtr)
```

#### 6
```c
typedef union {
	long long int bytes;
	int megabytes;
	short gigabytes;
	char terabytes;
} MemorySize;
```

#### 7
- 8 bytes (as big as largest member, `long long int`)

#### 8
- Yes it's valid code (will run with no error)
- No it will not make sense, because **`terabytes`** and **`bytes`** share the same memory
