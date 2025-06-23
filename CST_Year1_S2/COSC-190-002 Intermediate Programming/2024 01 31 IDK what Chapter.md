# Collections
### Data Structures
![600](Pasted%20image%2020240131080606.png)
### Java Collections
![600](Pasted%20image%2020240131080703.png)
### Java collection Heirarchy (java.util)
![](Pasted%20image%2020240131080747.png)
### Interfaces
![600](Pasted%20image%2020240131080936.png)
### All Collections will have
![400](Pasted%20image%2020240131081007.png)
### List Interface
![](Pasted%20image%2020240131081123.png)
![600](Pasted%20image%2020240131081139.png)
### List Iterator
![](Pasted%20image%2020240131081223.png)
![](Pasted%20image%2020240131081233.png)
### ArrayList
![](Pasted%20image%2020240131081256.png)
![](Pasted%20image%2020240131081311.png)
### Linked List
![](Pasted%20image%2020240131081556.png)
![](Pasted%20image%2020240131081611.png)
### Creating List Elements Quickly
![](Pasted%20image%2020240131081801.png)
### Comparator Interface
![700](Pasted%20image%2020240131084311.png)
### Collection Static Methods
![300](Pasted%20image%2020240131091539.png)
![](Pasted%20image%2020240131091549.png)
# In-Class Examples
*List.of makes the list Mutable (You can't change it after)*
You can use *Array.asList* to create a mutable list  
List.of Seems to create a immutable list
```Java
List<String> lstNames = List.of("Kevin","Ben","Dave","Dinkbot","Luckyllama");  
List<Integer> lstInts = List.of(19,22,33);  
List<Number> lstNums = List.of(17.2,19,-3,17.2);  
// Can't do List<String> lstNames2 = new List<>();

ArrayList<String> lstIns = (ArrayList<String>) List.of("Wade","Rick","Jason"); 
// Must cast as an ArrayList if you are doing it this way because ArrayList is a subclass of List
for(String sVal : lstNames) {  
    System.out.println(sVal);  
}  
  
lstInts.forEach(System.out::println);
```
#### Common Operations
```Java
// lstIns.set(1, "Coralee"); Replace element at index 1  
lstIns.add(1, "Coralee"); // Adds element at index 1 (bryce becomes index 2)  
lstIns.forEach(System.out::println);  
System.out.println("\n\n");  
  
lstIns.subList(1, lstIns.size()).forEach(System.out::println); // subList is the same as substring but for lists
```
#### ArrayList to normal Array
```Java
// Method 1 (Cast it as String[])
String[] saVals = (String[]) lstIns.toArray();  
lstIns.toArray(saVals);  

// Method 2 (No Cast, but need to predetermine memory)
String[] saVals2 = new String[lstIns.size()];  
lstIns.toArray(saVals2);
```
### Sorting an ArrayList
```Java
ArrayList<Dragon> lstDragon = new ArrayList<>();  
// Assuming we put some values in here  
lstDragon.sort(new compD());  // Need to make a comparator class for this to work obviously
// Second way to sort is is to use a LAMBDA statement  
lstDragon.sort((x,y) -> x.getSize().compareTo(y.getSize()));
// Third way to sort  
lstDragon.sort(Comparator.comparing(Dragon::getSize)); // Can make this any property of Dragon (color, size, name, etc.)
// Fourth sort method  
Collections.sort(lstDragon, (x,y) -> x.getAge()-y.getAge());
```
*compD* is a comparator method for the Dragon Object
if the IDE gets mad at you for trying to sort lstDragon, it's probably because it's empty right now, but it would work fine if it had elements in it
Basically they all do the same thing with slightly different syntax
### Making a generic method to generate a list of whatever you pass it based on the function
```JAVA
public static Function<String, Dragon> newDragon = x -> new Dragon(funcUtils.parseCSVLine(x));
```
Will take in a String and return a new Dragon based on parsing the CSV line
This method will take in a CSV file and return a list of whatever you want based on the function you pass it (In this case we will use the "newDragon" method above)
```Java
public static <T> List<T> genListLoad(String sFileName, Function<String, T> func)  
{  
    ArrayList<T> lstReturn = new ArrayList<>();  
    try(Scanner obIn = new Scanner(new File(sFileName)))  
    {  
        obIn.nextLine();  
  
        while(obIn.hasNextLine()) {  
            lstReturn.add(func.apply(obIn.nextLine()));  
        }  
  
    }  
    catch (Exception exp)  
    {  
        System.out.println(exp.getMessage());  
    }  
    return lstReturn;  
}
```
Then in main all you have to put is:
```Java
List<Dragon> lstDD= funcUtils.genListLoad("Files/Dragons.csv",newDragon);
```
To make a List of Cars instead, just make a function for Cars
```Java
public static Function<String, Car> newCar = x -> new Car(funcUtils.parseCSVLine(x));
```
and in main:
```Java
List<Car> lstCar = funcUtils.genListLoad("Files/car.csv", newCar);
```
#### Battleships
Make a Battleship object
Get the Battleships.csv file
make a function just like before but with your new Battleship object
gen the load list in main
print it out