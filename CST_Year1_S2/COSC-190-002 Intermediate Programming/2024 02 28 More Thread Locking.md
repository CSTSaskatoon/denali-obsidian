# Notes
Interrupted Exceptions are forced to be caught but "aren't necessary" according to Bryce
#### Semi Truck
Our basic logic for what we are doing today is that trailers ship goods in bulk to our warehouse, but we have a capacity of 7 items.
If the capacity is not enough for what the trailer has, it will wait until it does have space.
There is also a condition for the warehouse "not being empty", which we set after the trailer is done unloading
#### Delivery Truck
when a delivery truck arrives, if the amount it is requesting is too much for the capacity we have, it will await a "`notEmpty`" condition that signals it can now take from the capacity.
When the condition is met, it subtracts the capacity from the `currentCapacity`.
It then signals the "`notFull`" condition.
#### Simulating a day of delivery

# Code
#### `semiArrives` Method
```java
obLock.lock();  
  
try {  
    while (nCapacity + this.nCurrentCapacity > CAPACITY) {  
        System.out.printf("Semi Trailer Unit Delayed %d Current Capacity\n", nCapacity, this.nCurrentCapacity);  
        whNotFull.await();  
    }  
  
    this.nCurrentCapacity += nCapacity;  
  
    System.out.printf("Semi Trailer Unit Finished Cap is now %d\n",this.nCurrentCapacity);  
    whNotEmpty.signalAll();  
  
}  
// Bryce says InterruptedExceptions are stupid  
catch (InterruptedException ignored) {}  
finally {  
    obLock.unlock();  
}
```

#### `deliveryArrives` Method
```java
obLock.lock();  
  
try {  
    while(nCapacity > this.nCurrentCapacity) {  
        System.out.printf("Delivery Truck Waiting %d Current %d\n",nCapacity, this.nCurrentCapacity);  
        whNotEmpty.await();  
    }  
    this.nCurrentCapacity -= nCapacity;  
    System.out.printf("Delivery Truck leaves with %d cap is now %d\n",nCapacity, nCurrentCapacity);  
    whNotFull.signalAll();  
}  
catch (InterruptedException ignored) {}  
finally {  
    obLock.unlock();  
}
```
#### Useful bit of code to delay something happening before the pool is actually shut down
```java
obPool.shutdown();  
while(!obPool.isTerminated()) {}  
System.out.printf("Day is finished for semis");
```
*Just don't put anything inside the while loop*
