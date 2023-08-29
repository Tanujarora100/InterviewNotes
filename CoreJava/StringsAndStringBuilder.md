# Strings And Other String Related Classes


To perform String operations JAVA has predefined classes.
- java.lang.String
- java.lang.Stringbuffer
- java.lang.StringBuilder
- java.lang.StringTokenizer
- Most commonly used object is String object



## String Tokenizer
### What is StringTokenization and How it is possible to perform String Tokenization?

- process of dividing a string into number of tokens is called as String tokenization.
- Stringtokenizer class is in java.util.package.
- used mostly in lexical analysis.
- It is a legacy class.

### StringTokenizer Constructors
1. StringTokenizer(String str)->It creates StringTokenizer with specified string.
2. StringTokenizer(String str, String delim)->It creates StringTokenizer with specified string and delimiter.
3. StringTokenizer(String str, String delim, boolean returnValue)->It creates StringTokenizer with specified string, delimiter and returnValue. 
    - If return value is true, delimiter characters are considered to be tokens. If it is false, delimiter characters serve to separate tokens.

### **Method of StringTokenizer**

1. boolean hasMoreTokens()->It checks if there is more tokens available.
2. String `nextToken()`->It returns the next token from the `StringTokenizer object`.
3. String nextToken(String delim)->It returns the next token based on the delimiter.
4. boolean hasMoreElements()->It is the same as hasMoreTokens() method.
5. Object nextElement()->It is the same as nextToken() but its **`return type is Object.`**
6. int countTokens()->It returns the total number of tokens.
## **What is the Difference in == and equals Method?**

- == is the reference comparison operator
    - If the both Object are same then it will return true it checks the reference not the content of the strings.
- Object class Equals method() for reference/ address and same as == operator
    - In the child class the **equals method is overridden for Content comparison.**
    - In the Stringbuffer **class the equals method is not overridden and it checks the address only and not the content while in String class it is overridden**
    - **Wherever we need the equals method we need to override this in our class.**
- Equals Method
    - String Class- Content Comparison
        - String is immutable
    - **Stringbuffer Class- Reference Comparison**
        - Mutable in nature.
- toString() Method
    - String→Overriden
    - Stringbuilder→Overriden
    - StringBuffer→Overriden.

## What is the difference when we are using the new keyword to create string and when we are making the string using literals? 
### New Operator	
1. New Object is created in heap compulsory every time.
2. New Object will be created in String constant pool with no explicit reference variable to this SCP object.
    - This SCP Object is not for garbage collection as the implicit reference variable is present.
3. SCP Is stored in JAVA Heap space from java 7 onwards.
4. Heap Objects are eligible for GC while SCP objects are not eligible for GC. 
5. "" operator creates object in SCP while new operator creates an object in the `heap area(Method Area)`.
```java
public class Test{
    public static void main(String[] args)
    {
        String s1= new String("Tanuj");
         //2 Objects created with one line-> One In SCP and One in Heap
        String s2= new String("India");
        //2 Objects created with one line-> One In SCP and One in Heap.
        String s3= "Tanuj";
        //No object created
        String s4="India";
        //No object created
    }
}


```java
public class Test{
    public static void main(String[] args)
    {
        String A= new String("India");
        //2 Objects created
        A.concat("Software");
        // One created in SCP for Software and another concatenated string object with IndiaSoftware eligible for GC as there is no reference variable.

        A= A.concat("Industry");
        // One created in SCP for Industry and another concatenated string object.
        /*
        **SCP-3 Objects**

            - India
            - Software
            - Industry
        */
    }
}
```
```java
package String;

public class StringBuilder {
    public static void main(String[] args) {
        String s1 = new String("You Cannot change me");
        //1 object in heap one in SCP
        String s2 = new String("You Cannot change me");
        //One object in heap.
        System.out.println(s1 == s2);
        // false
        String s3 = "You Cannot change me";
        System.out.println(s1 == s3);
        // false
        String s4 = "You Cannot change me";
        System.out.println(s3 == s4);
        //true
//s3 and s4 pointing to same object.
        String s5 = "You Cannot" + "Chang me";
        // Concatenation is done at compile time and not run time
//The object at runtime is same as "You cannot change me"
//This will point to the same object as s4.
        System.out.println(s4 == s5);
        //true
/*

Therefore, s4 == s5 evaluates to true because s4 and s5 both point to the same string object in the string pool. The compiler optimizes the concatenation of string literals to ensure that they are reused from the pool whenever possible, which can improve memory efficiency and string comparison performance.

It's worth noting that this optimization only applies to string literals or constant expressions. If you use variables in the concatenation, the concatenation is performed at runtime, and the strings won't be automatically pooled. For example, the following will not be optimized:

java
*/
        String s6 = "You Cannot";
//One object in SCP area.
        String s7 = s6 + "Change me";
//As both are not constants there is one variable.
//Change me created in SCP area.
//New object created called "You Cannot Change me"
//This will be done at run time object.
//One new object in heap is made at runtime and they are not pointing to the same object.
        System.out.println(s7 == s4);
        //false
        final String s8="you Cannot";
//it is a constant
String s9= s8+ "Change me";
//This is done at compile time as final variable is a constant in itself, this total thing is now Same as" You Cannot change me"
System.out.println(s4==s9);
//true as both are same

    }

}
Heap
1- you cannot change me.
2-You cannot change me.


SCP-
You cannot change me
```
## Methods in String Class
1. public int length()-> length including spaces
2. String concat()-> concat in immutable manner.
3. public boolean equalsIgnoreCase()-> comparison between two strings.
4. public int compareTo()-> compares String in dictionary order
    - if str1 comes first=> returns -ve
    - if str2 comes first=> returns +ve
    - if both at the same position=> return 0 
```java
String str1 = new String("abc");
String str2 = new String("def");
String str3 = new String("abc");
System.out.println(str1.compareTo(str2));
System.out.println(str2.compareTo(str3));
System.out.println(str3.compareTo(str1));
    /*
    Output: -3
    3
    0
    */
```
5. public boolean startsWith(String str)=> Check string starting(takes string as parameter not character).
6. public boolean endsWith(String str)=> Check string ends with string.
7. public boolean contains(String str)=> Check string contains given string.
8. public String trim()=> remove pre spaces and post spaces
9. public String[] split(String str)=> split the string on the given delimiter or string and returns a **` String []`**.

### **What is the Difference in String and String buffer?**

- String objects are immutable
- String buffer objects are mutable in nature.

### **What is the Difference Between String and StringBuffer?**

- Stringbuffer→ JDK 1.0 Version
- StringBuilder→JDK 5.0 Version
- StringBuffer→Synchronized
- StringBuilder→Unsynchronized
- StringBuffer→Thread Safe
- StringBuilder→Not Thread Safe
- StringBuffer→Sequential Process
- StringBuilder→Parallel Process
- StringBuffer→Reduce application performance
- StringBuilder→Increase application Performance

### Why String sare immutable in Java?
1. String objects are stored in string pool and it is possible that multiple references are referring to the same object. So if we make it mutable then change in value done by any one reference will also affect the value referred by other references.
2. Security : String is made immutable to help increase security. Sensitive data like username, password can be stored as the Strings can’t be modified once created.
3. Class loading : String objects are used for Class loading. It is possible that wrong class has been loaded in the JVM, if the String is mutable i.e modifiable.

```java
public static void main(String[] args)
  {
        String s1=new String("Buggy");
               test(s1);
        System.out.println(s1);
        
  } 
 
 private static void test(StringBuffer s){
  s.append("Bread");
 }
 //Output=> Buggy
```

### Are String thread-safe in java?
- Ans: As we know, String objects are immutable. It means they are thread-safe because all immutable objects are thread-safe in java.

### How many different ways you can create a String object?

- You can create a String object using two ways. First is using new operator and second is using string literal. 
- Objects created using new operator are stored in the heap memory while string literals are stored in the string constant pool.
```java
String str = "javahungry";  // String literal
String str = new String("javahungry"); // using new operator
```
### Which class is final among String, StringBuilder and StringBuffer?
- All are final classes.

### Can we use String in switch statement?
- Yes, you can use String in switch statement in java 7. Prior to java 7 , you had to use if-else statements to achieve the task.
### What is String intern() method?


- When the intern method is invoked, if the String constant pool already contains a string equal to the String object as determined by the equals(Object) method, then the string from the pool is returned.
- Otherwise the String object is added to the pool and a reference to the String object is returned.
- The task of intern() method is to put String (which is passed to the intern method) into string constant pool.

### Is it possible to call String class methods using String literals?
- Yes, It is possible to call String class methods using String literals. 
```java
"javahungry".indexOf(u)
"javahungry".charAt(0)
"javahungry".compareTo("javahungry")
```