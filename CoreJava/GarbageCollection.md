## **What is Garbage in programming?**
Objects which we are not using are picked up by the garbage collector in java.

## **What is the need of a Garbage Collector in Java?**
In Old Languages like C++ programmers create the object and destroy the object manually using delete keyword.Usually Programmer taking very much care while creating objects and neglecting destruction of useless objects, at a certain point for creation of a new object sufficient memory may not be available (Because total memory filled with useless objects only),Total Application will be done due to memory problems, **hence out of memory error is very common in old languages like C++.**
Java releases the responsibility of deleting the useless objects called Garbage Collector.
Garbage Collectors are always running in the background which are called **Daemon threads.**

## **Where is the garbage Collector present?**
Garbage Collector is present inside the **JVM.**

## **How to make the Object Eligible for Garbage Collection?**
If an object does not contain any **reference variable** then that object is eligible for GC.

## **Ways to make an object eligible for Garbage Collection**

- Even though programmer is not responsible for destruction of object if it is no longer required, an object is said to be eligible for GC if and only if it does not contain any reference variable
- If an object does not have any reference variable then that object is **eligible for GC**.

## **In How many ways can we make the object eligible?**
### There are 4 ways in total.
#### **Nullifying the Object reference→**
- if not required now then assign null to a**ll reference variables then that object automatically eligible for garbage collection.** This approach is called **Nullifying the reference variable.**
```java
    public static void main (String[] args)
    {
        gc gc1= new gc();
        gc gc2= new gc();
        g1=null;
        g2=null;
    }
```
#### Reassign the reference variable
- If an object is no longer required then reassign the reference variable to some other object then old object by default eligible for garbage collection.
```java
public static void main (String[] args)
{
    GarbageCollector g1= new GarbageCollector();
    GarbageCollector gc1= new GarbageCollector();
    g1= new GarbageCollector();
    //old object will be under GC Now
    g2= g1;
    //old g2 object now under GC 
}
```
#### Objects created Inside a Method
- Objects created inside the method are automatically eligible for GC as soon as the method is completed executing.
```java
private static void Student()
{
    garbageCollector g1= new GarbageCollector();
    garbageCollector gc1= new GarbageCollector();
}

public static void main (String[] args)
{
    Student();
    //As soon the method is ended all the objects are gone
}
```
## **The methods for requesting JVM to run Garbage Collector**

- The ways to request a JVM to run a garbage collector, There are 2 ways in total.
- Once we make an object eligible for GC it may not be destroyed immediately by GC, whenever JVM runs a GC, then only the objects will be destroyed but when exactly JVM runs GC we cannot decide as it varies from JVM to JVM.
- Instead of Waiting for JVM to run a garbage collector, we can request a JVM to run GC programmatically, but whether JVM accepts our request or not there is no guarantee.
- But most of the time JVM accepts our request.
- There are 2 Ways to run GC:
    - By Using System Class- it contains a static method named System.gc() to request the garbage collector.
    - By Using Runtime class-Present in java.lang package
        - It is a singleton class so it follows a factory design pattern and returns only a single object.