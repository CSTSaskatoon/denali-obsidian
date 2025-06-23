# Typedefs and Function Pointers
## Typedef
- a tool to provide a synonym for an existing type
- Handled by the **compiler** (not the pre-processor)
- Doesn't create a new type in any sense, only adds a new name for some existing type
- Not any new semantics/meaning; variables declared this way have exactly the same properties as variables whose declarations are spelled out explicitly.
- `typedef` is like `#define`, except that since it's handled by the compiler it can copy with textual substitutions beyond the capability of the pre-processor. Ex. `typdef`s are used with function pointers

### Benefits
- Aesthetics
- Parameterize a program against portability issues. If typedefs are used for data types that may be machine-dependent, only the `typedefs` need to change when the program is moved. One common situation is to use `typedef` names for various integer quantities, then make an appropriate set of choices from `short`/`int`/`long` for each host machine.
- To provide better documentation for the program - a type called `TreePtr` may be easier to understand than one declared only as a pointer to a complicated structure

### Syntax
```c
typdef ExistingType NewType;
```

### Examples
#### Ex. 1
```c
typdef int Length;
// Makes the name Length a synonym for int. Length can be used in declarations, casts, etc.
// n exactly the same ways the int can be used

Length len, maxLen;
Length* lengths[];
```

#### Ex. 2
```c
typdef float REAL;

REAL x; // Same as float
```

#### Ex. 3
```c
typdef char* String;

// Makes String a synonym for char*, which may then be used in declarations and casts
String p, linePtr[MAXLINES];

int strComp(String, String);

p = (String)malloc(100);
```

#### Ex. 4
```c
typdef unsigned short Ushort;
```

#### Ex. 5
```c
typdef enum Boolean { False, True } BOOL;

BOOL amIDeadYet = False;
```

## Function Pointers
- Recall that we can print the address of a function by printing the function's name using the `%p` format specifier
- We can have pointers to functions
- A `typedef` can make function pointers easier to use

### Syntax
```c
typedef returnType(*SOMENAME)(parameter list);
```

### Example
```c
typedef int(*FNPTR_TYPE)(int);
```

### Where are they used?
- Callback functions - essentially like a delegate in C#
- Event handlers - internally implemented with function pointers
- Functions in objects are implemented with function pointers