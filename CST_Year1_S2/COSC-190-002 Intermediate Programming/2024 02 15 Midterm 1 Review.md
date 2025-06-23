By: Brody Crawford
# RegEx
(?i) - ignore case
all "*the* " with "_light_" following it
(?i)(\bthe\b) (?!light) - all "_the_" without "_light_" following it
(?i)(?<=the) (light) - all "_light_" as long as "_the_ " is before it
For CSV files, if you want to include commas in your phrase then you need to surround it in quotes. 
Pattern we will use for this - _,(?=([^\"]*\"[^\"]*\")*(?![^\"]*\"))_
# Exception
Checked:
An exception has to be in a try/catch block.
(try new File)

Unchecked:
Runtime exceptions don't need to be in a try/catch block.
(Divide by 0)
## Making exceptions
New class that extends Exception, or whatever exception your want to extend.
#### extend Exception
```java
public class MakingException extends Exception  
{  
    public MakingException()  
    {  
        this("Default message");  
    }  
      
    public MakingException(String message)  
    {  
        super(message);  
    }  
}
```
# File I/O
#### PrintWriter
```java
public static void writeFile(String sFileName)  
{  
    //If file doesn't exist, it will make it, otherwise write over it  
    try (PrintWriter obOut = new PrintWriter(sFileName))  
    {  
        obOut.println("This is some text");  
        obOut.println("Here is some more text");  
        obOut.print("This is the last line");  
    }  
    catch (IOException e)  
    {  
        e.printStackTrace();  
    }  
}
```
#### Scanner
```java
public static void readFile(String sFileName)  
{  
    try (Scanner obIn = new Scanner(new File(sFileName)))  
    {  
        while (obIn.hasNextLine())  
        {  
            System.out.println(obIn.nextLine());  
        }  
    }  
    catch (IOException e)  
    {  
        e.printStackTrace();  
    }  
}
```
#### File

### Binary writing, probably want to use with Data input stream
#### FileInputStream
```java
public static void readFile(String sFileName)  
{  
    try (FileInputStream obIn = new FileInputStream(sFileName))  
    {  
        while (obIn.available() != 0)  
        {  
            System.out.println(obIn.read());  
        }  
    }  
    catch (IOException e)  
    {  
        //If this is a GUI, add text to inform user  
        e.printStackTrace();  
    }  
}
```
#### FileOutputStream
```java
public static void writeFile(String sFileName)  
{  
    //Can read a file object to check if file is readable and not a directory  
    try (FileOutputStream obOut = new FileOutputStream(sFileName))  
    {  
        obOut.write(10);  
        obOut.write(4);  
        obOut.write(12);  
        obOut.write(15);  
    }  
    catch (IOException e)  
    {  
        e.printStackTrace();  
    }  
}
```

### Better structure - primitive types - UTF
#### DataInputStream
```java
public static void readFile(String sFileName)  
{  
    try (DataInputStream obIn = new DataInputStream(new FileInputStream(sFileName)))  
    {  
        System.out.println(obIn.readInt());  
        System.out.println(obIn.readBoolean());  
        System.out.println(obIn.readChar());  
        System.out.println(obIn.readDouble());  
    }  
    catch (IOException e)  
    {  
        e.printStackTrace();  
    }  
}
```
#### DataOutputStream
```java
public static void writeFile(String sFileName)  
{  
    try (DataOutputStream obOut = new DataOutputStream(new FileOutputStream(sFileName)))  
    {  
        //Cannot write objects  
        obOut.writeInt(1234);  
        obOut.writeBoolean(true);  
        obOut.writeChar('A');  
        obOut.writeDouble(12.5);  
    }  
    catch (IOException e)  
    {  
        e.printStackTrace();  
    }  
}
```

### Write whole objects (Using Cat Class in examples)
#### ObjectInputStream
```java
public static void readFile(String sFileName)  
{  
    //Object needs to "implements Serializable" (turn into a collection of bytes in a structure)  
    try (ObjectInputStream obIn = new ObjectInputStream(new FileInputStream(sFileName)))  
    {  
        Cat myCat = (Cat) obIn.readObject();  
  
        System.out.println(myCat.getName());  
        System.out.println(myCat.getAge());  
        System.out.println(myCat.getCost());  
        System.out.println(myCat.isMale());  
    }  
    catch (IOException e)  
    {  
        e.printStackTrace();  
    }  
    catch (ClassNotFoundException e)  
    {  
        //Program doesn't have the object  
        throw new RuntimeException(e);  
    }  
}
```
#### ObjectOutputStream
```java
public static void writeFile(String sFileName)  
{  
    try (ObjectOutputStream obOut = new ObjectOutputStream(new FileOutputStream(sFileName)))  
    {  
        //add f to double to make it a float  
        Cat myCat = new Cat("Meo",12,200.5f,true);  
  
        obOut.writeObject(myCat);  
    }  
    catch (IOException e)  
    {  
        e.printStackTrace();  
    }  
}
```

### Helps with streams
BufferedInputStream
BufferedOutputStream
(Covered later)
### Both read and write
#### RandomAccessFile
```java
public static void main(String[] args)  
{  
    try (RandomAccessFile raf = new RandomAccessFile("Files/ExampleRAF.dat","rw"))  
    {  
        //Write  
        raf.writeBoolean(true);  
        raf.writeBoolean(false);  
        raf.writeDouble(256.78);  
        String myStr = "This is a string";  
        raf.writeInt(myStr.length());  
        raf.writeUTF(myStr);  
  
        //seek  
        raf.seek(1);  
        raf.writeBoolean(true); //Cursor at position 2  
  
        raf.seek(0);  
  
        //read  
        System.out.println(raf.readBoolean());  
        System.out.println(raf.readBoolean());  
        System.out.println(raf.readDouble());  
        System.out.println(raf.readInt());  
        System.out.println(raf.readUTF());  
  
    }  
    catch (IOException e)  
    {  
        e.printStackTrace();  
    }  
}
```

# Sorting / Searching
With generics you will need to extends *Comparable* and use compareTo on the objects.
*Comparator* is compare(Object 1, Object 2).
Returns: <0, 0, >0
Check in reverse to get descending order.
### Binary Search
Sorted list, pick middle and see if value is smaller, larger, or equal
### Merge Sort
Split it up, then reorder it
### Insertion Sort
Find *smallest* element and check if any others are smaller. When it finds a smaller element it swaps places with it. It goes through the array only *swapping* the elements it runs through.
#### Insertion Sort
```java
public static void insertSort(int[] values)  
{  
    for (int i = 0; i < values.length; i++)  
    {  
        int indexOfSmallest = i;  
        for (int j = i+1; j < values.length; j++)  
        {  
            if (values[indexOfSmallest] > values[j])  
            {  
                indexOfSmallest = j;  
            }  
        }  
  
        //swap  
        int temp = values[i];  
        values[i] = values[indexOfSmallest];  
        values[indexOfSmallest] = temp;  
    }  
}
```
### Bubble Sort
Can also use it with largest element.
Don't check the elements that are already at the extreme ends (after sorted).
#### Bubble Sort
```java
public static void bubbleSort(int[] values)  
{  
    for (int i = 0; i < values.length; i++)  
    {  
        for (int j = i; j < values.length-1; j++)  
        {  
            if (values[j] > values[j+1])  
            {  
                //swap  
                int temp = values[j];  
                values[j] = values[j+1];  
                values[j+1] = temp;  
            }  
        }  
    }  
}
```

# Recursion
Have a base case.
Update your iterations.
Return when you your base case.
Linked list.
Converting integrative methods to recursive and vise Vera.
# Data Structures
Linked List
Stack
Queue
## Collections
### All Collections Will have
![400](Pasted%20image%2020240131081007.png)
### List
#### ArrayList
extends List
*Concrete Class*
Internally, it maintains an Array of the given type and grows as necessary
#### List Iterator
Allows you to traverse in both directions
#### `List.of`
useful if only working with a few elements
If you really need a concrete class you can cast it
**Makes the list Mutable (You can't change the List at all)**
#### `List` static methods
```
sort - sorts the list
binarySearch - does a binary search on the sorted list
reverse - reverses the list
reverseOrder - reverses the list based on a comparator
shuffle - randomly shuffles the list
copy - copies the list into a new list (must provide list to copy to)
nCopies - copies a specific element in the list that you specify, a number of times
fill - fills the list with whatever you specify
```
#### `Collections` static Methods (**All require a Collection to be passed to it, almost all will return an object**)
```
max - gives you the max from the Collection based on a Comparator
min - gives you the min from the Collection based on a Comparator
disjoint - checks if two Collections you pass to it have any common elements (returns boolean)
frequency - returns the frequency of an element specified in the Collection passed to it (returns int)
```
# Generics
### Notes about Generics
you can't create a new instance of a Generic Type, or a Generic Type Array (because they are converted at runtime)
- Can bypass this by using `Arrays.copyOf`, which works as long as you know the size of the array

You can't have a generic type parameter class in static context
Exception classes can't be generic
### Code
```java
<T>
<T,A>
<T extends Comparable<T>>
```
Can't have a Generic at runtime. It creates generics initially as Objects and casts them later.
Object array can hold generic types but the array itself is an Object array.
#### Generic Bubble Sort
```java
public static <T extends Comparable<T>> void bubbleGenericSort(T[] aVals)  
{  
    for (int i = 0; i < aVals.length; i++)  
    {  
        for (int j = i; j < aVals.length-1; j++)  
        {  
            if (aVals[j].compareTo(aVals[j+1]) > 0)  
            {  
                T temp = aVals[j];  
                aVals[j] = aVals[j+1];  
                aVals[j+1] = temp;  
            }  
        }  
    }  
}
```
# Lambda / Functions
T = Value the function takes in (Ex. an Integer)
U = Second Value the function takes in (Ex. an Integer)
R = Value the function returns
- Often a `List`/`ArrayList`/`Array`
- Can be something like an Integer if getting the max
- Also commonly a String

*Consumer`<T>`*
- Takes something in, doesn't output anything
- Like Print-line
- Method - `void accept(T t)`
- Syntax - `T->operation`

*Supplier`<R>`*
- Gives something, doesn't take anything in
- Like a getter
- Method - `R get()`
- Syntax - `()->R`

*Function`<T,R>`*
- Takes something in, and outputs something
- Method - `R Apply(T t)`
- Syntax - `T->return R`

*Predicate`<T>`*
- Takes something in, and returns a Boolean
- Method - `boolean test(T t)`
- Syntax - `T->True/False`

*BiFunction`<T,U,R>`*
- Takes in two parameters, returns one.
- Method - `R Apply(U,R)`
- Syntax - `(T,U)->Return R`

Consumer, function, and predicate have Bi versions which takes in *two* things.
Privative versions of these functions.
# Streams
*Main difference between Streams and Collections is that you can't edit a stream, it's just a bunch of values that you are stepping through that disappear once you go past them*

*Intermediate* operations are in between.
*terminal* operations are at the end.

*map* changes the data you are working with.
*filter* will filter the data based on a predicate.
*distinct* finds unique values.
*sorted* will sort and by default use a comparator.
*limit* will limit your stream to the number of values.

*count* return a long value of how many values there are.
*toArray* will collect values into some sort of array of Objects.
*toList* is a collect shorthand to make a List.
*Collect* lets you collect the data is many different ways.
- Collectors.toCollection(ArrayList::new)
- Could also collect into different collections class
- *groupingBy* is makes a map, allowing key/value pairs, Must be assigned to a *Map*<Map type, Value type>

*forEach* is a void that lets you use a intermediate operation or a terminal operation.
you can have as many intermediate operations as you want, but only one terminal operation
### Mapping
![](Pasted%20image%2020240215165206.png)
Essentially, mapping is like casting the object you are currently looking at in the stream to some other value
In this example, this map should return a list of just each car's price
# Things to Go Over
### Generic Types and Wildcard types
![500](Pasted%20image%2020240116090816.png)
![600](Pasted%20image%2020240116090907.png)
You can't have a generic type parameter class in static context?
#### Example
`Integer`, `Float`, and `Double` all extend `Number`.
