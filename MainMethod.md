Requirement of the Main Method()
--------------------------------

-   Defining Program Start and End: The main method serves as the entry point of a Java program, indicating where the program starts and ends.

-   Managing Application Logic: It provides a location to manage the application's logic in Java programs. The main() method is automatically executed by the Java Virtual Machine (JVM).

Type of Method: main Method()
-----------------------------

-   Not Predefined or User Defined: The main method is not a predefined method like those in Java's standard libraries, nor is it user-defined in the traditional sense.

-   Conventional Method: It's a conventional method with a fixed prototype but allows for user-defined implementation.

-   Reason for Flexible Implementation: The flexibility in implementing the main method is intentional to accommodate varying user requirements.

Requirement to Declare main Method as Public()
----------------------------------------------

-   Starting the Application: The main method is mandatory for starting a Java application, hence it requires an accessible scope.

-   Bringing Scope to JVM: To make the main method accessible to the JVM, it must be declared as `public`.

-   Public Access for JVM: Since the main method call is vital for starting the application, it needs to be accessible to JVM, which operates outside the application package.

-   Access Modifiers Explained:

    -   Private: Limited to the current class, inaccessible to JVM.
    -   Default (package-private): Accessible within the current package only, thus not accessible to JVM.
    -   Protected: Accessible within the current package and by child classes in other packages, but not by JVM.
-   Why Public?: Declaring the main method as public makes it accessible throughout the system, including JVM and Java software.

Declaring main Method without Public
------------------------------------

-   Compilation Behavior: Declaring the main method without `public` won't lead to a compilation error; the compiler treats it as a normal method.

-   Runtime Behavior (pre-Java 7): If the method is not public, up to Java 6, there's no issue at compile time. However, at runtime, the JVM will not find the main method.

-   Runtime Behavior (Java 7 and Later): Starting from Java 7, if the main method is not public, a compilation error occurs: "Main Method not found in class 'NAME OF CLASS', please define the main method as public static void main(String[] args)."

What is the requirements to declare main() as static?
-----------------------------------------------------
- Instance methods can be accessed using objects only.

- Static methods can be accessed using:

    - Class name- used for static methods.

    - reference variables- it may be static or may be instance methods.

- As Per JVM Implementation, it should be declared as static as it access the main method using CLASS NAME.

    - JVM Implementation was designed in this way---> to make it lightweight, creating object requires more memory---> Making JVM Heavier---> performance is reduced.

- If we declare main method without static?
- No Compilation error---> Simple method for compiler

Error: Could not find or load main class .\oopsClass.class
Caused by: java.lang.ClassNotFoundException: /\oopsClass/class Please declare the main method  as static.
