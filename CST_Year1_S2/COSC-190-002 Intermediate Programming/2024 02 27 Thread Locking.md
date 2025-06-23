# Notes
### Thread Locking
Instead of doing delays to prevent threads from doing weird shit, you can lock them
#### Cooperation
*await()* - void (Makes the current thread wait until the condition is signalled)
*signal()* - void (wakes up one waiting thread)
*signalAll()* - Condition (wakes up all waiting threads)
Basically, with this you can create a "Condition" that allows you to sleep and wake threads when certain things happen really easily instead of relying on timed intervals
# Code
### Thread Locking
#### Account Class
```JAVA
public static class account  
{  
    public account() {  
        balance = 0;  
    }  
    int balance;  
    private static Lock obLock = new ReentrantLock();  
  
    public synchronized void addAPenny() {  
        obLock.lock(); // Thread will attempt to aquire lock  
        int nNewBalance = balance + 1;  
        balance = nNewBalance;  
        obLock.unlock();  
    }  
    public int getBalance() {  
        return balance;  
    }  
}
```
In this example, we use a *ReentrantLock* to prevent the method from running at the same time as another thread and incorrectly adding pennies.
#### Thread Cooperation
##### Withdraw Method
```java
public void withdraw(int nAmount)  
{  
    obLock.lock();  
    try {  
        while(balance<nAmount) {  
            System.out.printf("\t\tWait for deposit\n");  
            newDeposit.await();  
        }  
        balance -= nAmount;  
        System.out.printf("\t\tWithdraw: %d\tBalance is now %d\n",nAmount, this.balance);  
  
    }  
    catch (InterruptedException ignored) {  
  
    }  
    finally {  
        obLock.unlock();  
    }  
}
```
##### Deposit Method
```java
public void deposit(int nAmount)  
{  
    obLock.lock();  
    try {  
        this.balance += nAmount;  
        System.out.printf("\t\tDeposit %d\t\t\tBalance: %d\n",nAmount, this.balance);  
        // Signal any thread that is waiting for deposit that it is good to proceed  
        newDeposit.signalAll();  
    }  
    finally {  
        obLock.unlock();  
    }  
}
```
