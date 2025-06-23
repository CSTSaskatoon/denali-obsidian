# Threads
Can be thought of as small programs that can be started up from another program
- Don't require the overhead of a complete program

These threads don’t necessarily run in the exact manner that you might expect
Let’s look at a thread model and how a single CPU might deal with a thread 
- Note that threads must wait for their turn at the CPU (notion of multitasking) 
- A thread does not run to completion in the CPU - if it does not finish and it ‘s time quota is up - It will have to wait for another crack at the CPU.
### Life cycle of a thread
![](Pasted%20image%2020240213080715.png)
### Terms
Runnable - A thread that is ready to run is in the runnable state
-  It is the duty of the OS to schedule this thread to run at some time 
	- Round Robin Scheme 
	- Priority Round Robin 

Running - A thread that is “in” the CPU and is executing
- Normally threads will execute for a variable length of time (as per the scheduler) in the CPU and then voluntarily give up CPU and migrate back to the Runnable State
- Threads will tend to ping pong back and forth from the Running to the Runnable State.
#### Other States
Blocked - Typically this involves the thread waiting for some resource to become available 
	- Disk Drive -  Printer 

- A thread will not move back into the runnable state until that resource becomes available
- Note that a shared resource between threads could also involve them moving into a blocked state (A has Resource, B wants resource) 

Waiting - This occurs when a thread invokes the Join method on its sub threads 
- It is waiting for them to finish before proceeding

Timed Waiting - Typically this involves the thread putting itself to sleep for some amount of time
- Usually involved by calling the sleep() method
### Modern systems
Most modern CPUs have multiple cores, typically each core will be capable of running 2 threads
- it's the job of the compiler to set up the code and take advantage of this

If you want to see the number of threads available to your system you can utilize a static method associated with a Runtime object to get
- `RunTime.getRunTime().availableProcessors() * 2`
### Thread Synchronization
A thread (the main runs as a thread on the system) can be made to wait for other threads to finish by “joining the thread". Let’s look at another example of this
Note that the threads still run in random order
- Now the main thread must wait for the other threads to finish (via the Joins) before executing the last println statement 
- The join action forces the main thread to deal with an Interrupted Exception
### Anonymous Runnable Class
![400](Pasted%20image%2020240213090840.png)
### Sleeping
We can use Thread.sleep to timeout which works similar to javascript
- Causes the current thread to Sleep for the given number of milliseconds
- Static method

Can be used for simulations to mimic real world tests
- For example, we might want to figure out how many bank tellers are optimal for people visiting the bank (ignore automate tellers for time being)
- We can set up threads to simulate both tellers and customers and maybe have our factors set to be 10 to mimic a full seconds
	- Our simulation will run 100 times faster
### Setting Priority of Threads
Higher number = higher priority
Not super noticeable if the difference of priority isn't high enough
# Code
#### Runnable Class (Use to initialize Threads)
```java
private static int nValToPrint;  
  
public PrintNumber(int nVal)  
{  
    nValToPrint = nVal;  
}  
  
@Override  
public void run()  
{  
    for(int i=0;i<100; i++) {  
        System.out.print(nValToPrint + " ");  
    }  
}
```
#### Creating a Thread with our Runnable Class
```java
Runnable run21 = new PrintNumber(21);  
Runnable run27 = new PrintNumber(27);  
  
Thread thThree = new Thread(run21);  
Thread thFour = new Thread(run27);  
  
thThree.start();  
thFour.start();  
System.out.println("Main program finished");
```
*If you run this, it prints out the "Main program finished" before the Threads are done*
#### This WOULD fix the problem if `thThree` was in the try block
```java
Runnable runA = new PrintChar('A');  
Runnable runB = new PrintChar('B');  
Runnable runC = new PrintChar('C');  
  
Thread thOne = new Thread(runA);  
Thread thTwo = new Thread(runB);  
Thread thThree = new Thread(runC);  
  
thOne.start();  
thTwo.start();  
thThree.start();  
  
// Wait for the threads to finish  
try {  
    thOne.join();  
    thTwo.join();  
} catch (InterruptedException e) {  
    throw new RuntimeException(e);  
}  
System.out.println("Main program finished");
```
#### Create a Thread with a LAMBDA expression (No need for Runnable class)
```Java
Thread thOne = new Thread(() -> {  
    for(int i=0; i<100; i++) {  
        System.out.print("A ");  
    }  
});  
Thread thTwo = new Thread(() -> {  
    for(int i=0;i<100;i++) {  
        System.out.print("B ");  
    }  
});  
thOne.start();  
thTwo.start();
```
#### Creating a thread with a method (No Runnable Class)
```java
public static void main(String[] args)  
{  
    new Thread(() -> {  
        printChar('A');  
    }).start();  
    new Thread(() -> {  
        printChar('B');  
    }).start();  
}  
  
public static void printChar(char cVal) {  
    for (int i = 0; i < 100; i++) {  
        System.out.print(cVal + " ");  
    }  
}
```
#### This method will not work
```java
public static int i=0;  
public static void main(String[] args)  
{  
    char cVal = 'A';  
  
    for (; i < 5; i++) {  
        new Thread(() -> {  
            DemoSix.printChar((char) (cVal + i));  
        }).start();  
    }  
}
```
*The reason it doesn't work is because when you start it up, i = 0, but when the Thread executes it's different*
##### This method also does not work for the same reason
```java
public static int i=0;  
public static void main(String[] args)  
{  
    char cVal = 'A';  
  
    for (; i < 5; i++) {  
        new Thread(() -> {  
            final int nVal = i;  
            DemoSix.printChar((char) (cVal + nVal));  
        }).start();  
    }  
}
```
*There is a way to fix this in the future, but we can't do anything about it right now*
*The way to fix this is to create an object which controls the access to it*
#### Blastoff Class
```java
public static void main(String[] args)
{  
    for(int i=10;i>0;i--) {  
        System.out.println(i);   
    }  
    System.out.println("FUCK");  
}
```
*Issue with this is it executes everything immediately*
##### To fix this
```java
public static void main(String[] args) throws InterruptedException  
{  
    for(int i=10;i>0;i--) {  
        System.out.println(i);  
        Thread.sleep(1000);  
    }  
    System.out.println("FUCK");  
}
```
*Fixes the issue by sleeping the thread*
**Needs to either Throw or catch an InterruptedException**
#### Sleep Threads on the printChar Example
```java
public static void printChar(char cVal) {  
    for (int i = 0; i < 100; i++) {  
          
        if(cVal == 'A') {  
            try {  
                Thread.sleep(10);     
            }  
            catch (InterruptedException exp) {  
                  
            }  
        }  
        System.out.print(cVal + " ");  
    }  
}
```
*Essentially waits 10ms for each time it prints out an 'A'*
#### Setting Priority for Threads
```java
Thread thOne = new Thread(() -> {  
    DemoSix.printChar('C');  
});  
Thread thTwo = new Thread(() -> {  
    DemoSix.printChar('B');  
});  
  
thOne.setPriority(1);  
thTwo.setPriority(10);  
  
thOne.start();  
thTwo.start();
```
*Higher value gets printed first*
*Sometimes you get lower priority values in the mix, but it works fairly well*
*Difference is much more noticeable if you have a higher difference between the priorities*