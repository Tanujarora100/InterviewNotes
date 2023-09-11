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
 public class SingletonPattern {
    private static SingletonPattern instance = null;

    private SingletonPattern() {
    }

    public static SingletonPattern getInstance() {
        if (instance == null)
            instance = new SingletonPattern();
        return instance;
    }
}
class Main{
    public static void main(String[] args) {
        SingletonPattern obj = SingletonPattern.getInstance();
        System.out.println(obj.hashCode());
        SingletonPattern obj2= SingletonPattern.getInstance();
        System.out.println(obj2.hashCode()) ;
    }
}

```

## Lazy Loading with Double null check
```java
class MultithreadSingleton {
    private static MultithreadSingleton instance = null;

    private MultithreadSingleton() {
    }

    public static MultithreadSingleton getInstance() {
        if (instance == null) {
            //Our method is static so we are using class level locking here.
            synchronized (MultithreadSingleton.class) {
                //As this block is synchronized only one thread can come inside and exeucte it.
                if (instance == null) {
                    instance = new MultithreadSingleton();
                }
            }
        }
        return instance;
    }
}

```
- Advantages:
    - Memory usage
    - Thread Safety
- Disadvantage:
    - can be broken by reflection API.

## How to Break Singleton?
### Using ObjectStreams

```java
public class BreakSingleton implements Serializable {
    class SingletonPattern implements Serializable {
    private static SingletonPattern instance = null;

    private SingletonPattern() {
    }

    public static SingletonPattern getInstance() {
        if (instance == null)
            instance = new SingletonPattern();
        return instance;
    }
}
    private static void example() throws IOException, ClassNotFoundException {
        SingletonPattern singletonPattern= SingletonPattern.getInstance();
        ObjectOutputStream oos= new ObjectOutputStream(new FileOutputStream("Abc.txt"));
        oos.writeObject(singletonPattern);
        oos.close();
        ObjectInputStream ois= new ObjectInputStream(new FileInputStream("Abc.txt"));
        SingletonPattern oisSingleton= (SingletonPattern) ois.readObject();
        ois.close();
        System.out.println(oisSingleton.hashCode());
        System.out.println(singletonPattern.hashCode());

    }
    public static void main(String[] args) throws IOException, ClassNotFoundException {
        example();
    }
}
```
## How to Solve this then?
- Override the ReadResolve Method in the Singleton class.

```java
public class SingletonPattern implements Serializable {
    private static SingletonPattern instance = null;

    private SingletonPattern() {
    }

    public static SingletonPattern getInstance() {
        if (instance == null)
            instance = new SingletonPattern();
        return instance;
    }

    protected Object readResolve() throws ObjectStreamException {
        return instance;
    }
}
```
#### What is this Read Resolve Method?
- The readResolve method is a special method in Java that you can implement when a class is serializable. It allows you to control the process of object deserialization and specify what object should be returned when an instance of the serialized class is deserialized. This method is called by the Java Object Serialization mechanism during deserialization.
- If the class defines a readResolve method, the readResolve method is invoked immediately after deserialization, and its return value is used as the actual deserialized object.
- You can use the readResolve method to specify what object should be returned. In the case of a Singleton pattern, you return the existing Singleton instance to ensure that there's only one instance of the Singleton class.


### Using Reflections API
```java
package CreationalDesignPattern.Singleton;

import java.lang.reflect.Constructor;
import java.lang.reflect.InvocationTargetException;

public class ReflectionBreakPattern {
    private static void breakSingleton() throws InvocationTargetException, InstantiationException, IllegalAccessException {
        Constructor[] constructors= SingletonPattern.class.getDeclaredConstructors();
        Constructor privateConstructor= constructors[0];
        privateConstructor.setAccessible(true);
        SingletonPattern singletonPattern= (SingletonPattern) privateConstructor.newInstance();
        SingletonPattern newObject= SingletonPattern.getInstance();
        System.out.println(newObject.hashCode());
        System.out.println(singletonPattern.hashCode());
    }

    public static void main(String[] args) throws InvocationTargetException, InstantiationException, IllegalAccessException {
        breakSingleton();
    }
}

```
### Best Way to make Singleton
#### ENUMS
```java
package CreationalDesignPattern.Singleton;

public enum EnumSingleton {
    INSTANCE;

    public void singleton() {
        System.out.println("HELLO");
    }
}

```
### Why Enums are considered safe?
- Implicit Singleton: Enum constants are implicitly singletons. 
    - In Java, each enum constant is instantiated only once when the enum class is loaded, ensuring that there is only one instance of each constant throughout the lifetime of the application.
- Thread Safety: Enum constants are inherently thread-safe. Java ensures that enum constants are created in a thread-safe manner, and you don't need to worry about race conditions when accessing them from multiple threads.

- Serialization Safety: Enums are inherently serializable. 
    - When you serialize an enum object and then deserialize it, Java guarantees that you will get the same instance, preserving the Singleton pattern. 
    - This is because enum instances are identified by their names, not by their serialized state.

- Reflection Safety: Enums are immune to reflection attacks. Traditional Singleton implementations can be susceptible to being bypassed by reflection, but enum-based singletons cannot be instantiated via reflection. 
    - Any attempt to create a new instance of an enum using reflection will result in an exception.
    - Enum constructors are called internally by JVM and we cannot call them using Refelection.

- No Need for Synchronization: Enum-based singletons don't require explicit synchronization mechanisms like synchronized blocks or volatile variables, which are often needed in other Singleton implementations to handle lazy initialization and prevent race conditions.

