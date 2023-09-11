# Exception Handling

## What is Exception
- Exception is an unexpected event occurred in java applications at runtime , which may be provided by users while entering dynamic input in java applications, which maybe provided by database engine, maybe by network causes abnormal termination to the application.


## What is an Error?
- Compile Time errors
- i. Lexical Errors
    - int i=10; ----> Valid
    - nit i=10; ----> Invalid
- ii. Syntax Errors
    - int i=10;---> Valid
    - i int 10 ;-->Invalid
- iii. Semantic Errors
    - EX: int i=10;
    - boolean b=true;
    - char c= i+b;----> Invalid.

## What are Runtime errors
    - These are the problems for which we are unable to provide solutions programmatically and these errors are not identified by the compilers and these errors are occurred at runtime
    - Insufficient Main Memory
    - Unavailability of IO Components

## What is Finally Block?
- Finally: this block is always performed irrespective of the catching of exceptions in the try or catch block.

## Which class is the parent of all exceptions?
- Throwable Class

## What is the difference in Error and Exception?
- Errors typically happen while an application is running. For instance, Out of Memory Error occurs in case the JVM runs out of memory. We cannot handle errors as a programmer.
- On the other hand, exceptions are mainly caused by the application. For instance, Null Pointer Exception happens when an app tries to get through a null object.

## What is the difference in Checked and Unchecked Exception?
- Checked: Occur during the compilation. Here, the compiler checks whether the exception is handled and throws an error accordingly.
    - Monitoring done at compile time but exception is thrown at runtime only.
    - Compiler can predict the exception can come but exceptions do not come at compile time , exception always comes at runtime only.
        - SQL Exception
        - IO Exception
        - ClassNotFoundException
- Unchecked: Occur during program execution. These are not detectable during the compilation process.

## Types of Checked Exceptions
- Pure checked Exception
    -  If any checked exception is having only checked exceptions as sub classes then this Exception is called as Pure Checked Exception.
        - EX: IOException
        - SQL Exception
        - ClassNotFoundException
        - IllegalAccessException

- Partially checked Exception
    - If any Checked Exception contains at least one sub class as unchecked exception then that Checked Exception is called as Partially Checked Exception.
    - Example: Exception, Throwable
        - Exception and Throwable are partially checked because they have runtime exception as the child class
        - Throwable Class is the parent of both error and runtime exception.

## Unchecked Exception
- Unchecked Exceptions are not recognized at compilation time, these exceptions are recognized at runtime by JVM.
    - Error and Child classes.
    - Runtime Exceptions and Child Classes
    - Arithmetic Exception
    - NullPointer
    - Class Cast Exception
    - IndexoutofBound

## Can we Use try block alone?
- No a Compile time error will come as the catch or finally block must accomapny , we can remove either but never both.
- Note : From Java 7, with the introduction of try-with resources blocks, we can write only try block without catch and finally blocks provided resources must be AutoCloseable.


## What is the difference in Finally, final and finalize?
### finally
- finally is a keyword used in exception handling to define a block of code that will be executed regardless of whether an exception is thrown or not.
- It is typically used in conjunction with try-catch blocks to ensure that certain cleanup or closing operations are performed, such as closing a file or releasing 
```java
try {
    // Code that may throw an exception
} catch (Exception e) {
    // Handle the exception
} finally {
    // Code that will always be executed
    // e.g., resource cleanup
}

```
### final keyword
- final is a keyword used to declare a variable, method, or class as unchangeable or immutable.
- When applied to a variable, it means the variable's value cannot be modified once it is assigned. When applied to a method, it means the method cannot be overridden in subclasses. When applied to a class, it means the class cannot be extended (subclassed).
### finalize :
- finalize is a method defined in the Object class in Java, and it is used for garbage collection-related tasks.
- It allows an object to perform cleanup operations just before it is destroyed and collected by the garbage collector. However, it is generally discouraged to use finalize because it can lead to unpredictable behavior and performance issues.
- It's important to note that starting from Java 9, the finalize method has been deprecated, and it's recommended to use other mechanisms like the java.lang.ref.Cleaner class for resource cleanup instead.

## Number Format Exception
- unchecked exception
- In Java, NumberFormatException is an exception that is thrown when a method that parses a string into a numeric type encounters a string that cannot be converted to a valid number format. 
- This typically occurs when trying to convert a string to a numeric type like int, double, float, long, etc., using methods like Integer.parseInt(), Double.parseDouble(), Float.parseFloat(), or similar parsing methods.

## Define Rethrowing in Exception Handling?
- 

## What is Unreachable Catch Block in Java?
- When you are keeping multiple catch blocks, the order of catch blocks must be from most specific to general ones. i.e sub classes of Exception must come first and super classes later. 
- If you keep super classes first and sub classes later, compiler will show unreachable catch block error.
```java
public class ExceptionHandling
{
    public static void main(String[] args)
    {
        try
        {
            int i = Integer.parseInt("abc");   //This statement throws NumberFormatException
        }
        catch(Exception ex)
        {
            System.out.println("This block handles all exception types");
        }
        catch(NumberFormatException ex)
        {
            //Compile time error
            //This block becomes unreachable as
            //exception is already caught by above catch block
        }
    }
}
```

## What is the difference between StackOverflow and OutOfMemoryError?
- Stack overflow is related to stack while outOfMemory is related to heap overflow.
- stackoverflow due to alot of methods, heap memory due to objects.


## What is the difference between throw, throws and throwable in java?

## Can we keep the statements after finally block If the finally block is returning the control?
- No, it gives unreachable code error. Because, control is returning from the finally block itself. Compiler will not see the statements after it. That’s why it shows unreachable code error.
```java
public class FinallyReturnExample {
    public static void main(String[] args) {
        int result = divideAndReturn();
        System.out.println("Result: " + result);
    }

    public static int divideAndReturn() {
        try {
            int numerator = 10;
            int denominator = 0;
            return numerator / denominator;
        } catch (ArithmeticException ae) {
            System.err.println("ArithmeticException: " + ae.getMessage());
            return -1;
        } finally {
            System.out.println("Finally block executed");
            // The following return statement will not compile, as it's not allowed.
            // return 0; // This would result in a compilation error.
        }
    }
}

```
###  Does finally block get executed If either try or catch blocks are returning the control?
- Yes, finally block will be always executed no matter whether try or catch blocks are returning the control or not.
## What is the difference between ClassNotFoundException and ClassDefinitionNotFound Exception?
- ClassNotFound Exception is a `**checked exception**` when ClassLoader.loadClass() or class.forName() is used
    - occurs when classpath is not updated with required JAR Files.
- NoClassDefFoundError-It is an `**error**` not an exception when JVM tries to load a class which was available at compiletime but now not there at runtime.

## What is rethrowing an exception?
- Rethrowing an exception in Java is a technique where you catch an exception in one part of your code using a try-catch block and then throw the same exception again, either to propagate it up the call stack or to wrap it in a different exception type while preserving information about the original issue. 
- Rethrowing is commonly used when you want to handle exceptions at a lower level of your code but still want to report or handle them differently at a higher level.
```java
public class RethrowExample {
    public static void main(String[] args) {
        try {
            someMethod();
        } catch (Exception e) {
            System.err.println("Caught an exception: " + e.getMessage());
            // Rethrowing the caught exception as a new one
            throw new CustomException("Custom exception message", e);
        }
    }
    
    public static void someMethod() throws CustomException {
        try {
            // Code that may throw an exception
            int result = 10 / 0; // This will throw an ArithmeticException
        } catch (ArithmeticException ae) {
            System.err.println("ArithmeticException: " + ae.getMessage());
            throw ae; // Rethrowing the same ArithmeticException
        }
    }
}

class CustomException extends Exception {
    public CustomException(String message, Throwable cause) {
        super(message, cause);
    }
}

```