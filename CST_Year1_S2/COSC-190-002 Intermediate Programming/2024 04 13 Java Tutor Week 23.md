# Notes
## Blocking Queue
**Can use `arrayQueue.poll()` instead of `.take()` because `.take()` throws an error**
*`ArrayBlockingQueue`* has it's own lock

## File Server/Sockets
*was talking about closing DataInput/Output streams and the Socket connection, not entirely sure if it's required*
*Also talked about doing `obOut.flush()`*
- Sends the array of byte data even if the buffer isn't full
- *Still not sure what this means, but apparently you can have issues with it not sending data if you don't use it because the buffer isn't full*
- Use if you are writing small amounts of data

## JavaFX Image Flipper


# Code
## Blocking Queue
### `public static void addThreadQueue`
```java
while(true) {  
    try {  
        Random rand = new Random();  
        arrayQueue.put(rand.nextInt(1,101));  
        Thread.sleep(500);  
          
    } catch (InterruptedException e) {  
        e.printStackTrace();  
    }  
}
```
*Adds a random Integer to the queue every second*
### `public static void countQueueThread`
```java
while(true) {  
    System.out.println(arrayQueue.size());  
    try {  
        Thread.sleep(500);  
    } catch (InterruptedException e) {  
        e.printStackTrace();  
    }  
}
```
*Prints remaining capacity of the queue every second*
### `public static void consumeQueueThread`
```java
while(true) {  
    try {  
        Integer nVal = arrayQueue.poll();  
        if(nVal != null) {  
            System.out.printf("Value %d * 2 is %d\n",nVal,nVal*2);  
        }  
          
        Thread.sleep(1500);  
    } catch (InterruptedException e) {  
        e.printStackTrace();  
    }  
}
```
*Gets the head from the queue with `.poll()` every second and a half*
## File Server/Sockets

## JavaFX Image Flipper
