## How to create Singleton pattern?
- First create a private constructor-->Restrict the object creation outside of the class.
- We need to make a private class attribute of the class and make it static
- Reasons to Make it static:
    - By having it static, can be accessed anywhere--> Using SingletonClass.getInstance()
    - By making it static we make sure only one object is created and can control the object creation of the class.
    - Lifetime management of the object is easier and consistent during the program execution.
    - As the instance if static it acts as a global point of access to use the singleton class.

## Reasons to make the class instance private:
- Encapsulation: By making the instance variable private, you encapsulate the instance within the Singleton class itself. 
- This encapsulation prevents external classes from directly modifying or replacing the instance, which is crucial for maintaining the pattern's intended behavior of having a single instance.
- Controling Object Creation: Lazy Initialization or Eager Initialization.
    - To get the object of the class, we need a static method to get the instance.
- A Static method can be called by using class name without creating an object.
    - The Object cannot be created as the constructor is private.
- We cannot inherit a class with private constructor and then use child objects to call the parent class it is not allowed.

```java
public class SingletonClass {
    private static final SingletonClass instance = null;

    private SingletonClass() {
    }

    public static SingletonClass getInstance() {
        if (instance == null) {
            System.out.println("INVOKED ONCE");
            instance = new SingletonClass();
        }
        return instance;
    }
}
```
## Ways to create singleton class:
### Eager Loading
- When we are creating the object and initialiazing it before hand.
- The classloader will put load all the static methods and variables beforehand.
- Advantages:
    - Thread Safe in nature
    - Guaranteed Availibility
    - Avoids lazy loading overhead
- Disadvantages:
    - Resource Consumption.
    - Startup delay--> if object creation is time consuming.
    - Less Flexibile--> No control on when it needs to be created
```java
public class SingletonClass {
    private static final SingletonClass instance = null;

    private SingletonClass() {
    }

    public static SingletonClass getInstance() {
        if (instance == null) {
            System.out.println("INVOKED ONCE");
            instance = new SingletonClass();
        }
        return instance;
    }
}
```
### Lazy Loading
- Advantages:
    - Fast Startup
    - Flexible Initialization
    - Controller Instance Creation
- Disadvantage:
    - Not thread safe.
    - Complexity is increased--> Due to multithreading
    - Synchronization Mechanisms overhead.

```java
class LazyLoading {
    private static LazyLoading instance = null;
    private LazyLoading() {
        //Singleton class
    }

    public static LazyLoading getInstance() {
        if (instance == null)
            instance = new LazyLoading();
        return instance;
    }
}
```
