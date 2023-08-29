# MAIN METHOD
## What is the Requirment of the main method?
- To define starting point and ending point of the program that is one reason we need the main method.
- To  manage application logic in java applications we need the main() method which is executed automatically by JVM.

## What type of method is the main method?
- It is not a predefined methor or user defined method.
- It is a **`CONVENTIONAL`** Method with fixed prototype and with user defined implementation.
 
## Why the scope of the main method is public?
  - To start the application, JVM needs to find the main method as JVM is in a different package and the Main class maybe in a different package to find the main method , sun microsystems made this method **public** in scope.
  - If we declare it as Public then it is accessible throughtout the our system including java software and JVM therefore it must be public.

## Is is possible to have more than one main method in one class?
  - No, it is not possible to have more than one main method in same class.
  - We can have Main method in different classes and during command line we can give the path of the class where the main method is located.
 
## Why the main method is named main?
   - To show the importance of the method it is named as main.
 
   
  ## If we remove static keyword from main method then what happens?
    - No compilation error as this is just a normal method for Compiler.
    - But for JVM, it is a special method so in java 6 - `java.lang.NoSuchMethodError ` comes and in java 7 and above `Error: main method is not static in class Please define the main method as public static void main(String[] args)`.
     
