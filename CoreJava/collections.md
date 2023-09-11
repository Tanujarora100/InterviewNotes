# Collections In Java
## What is a Collection and What is Collection Framework?
- Collections is an object, it is able to manage a group of Objects a single entity.
- Package—> java.util
### What is the difference in Collection and Collections?

- Collection:
    - It is an **interface in java.util** package
    - It is a general purpose interface with methods like add, remove, access
    - List Interface, Set interface, Queue Interface implements this interface
- Collections:
    - It is a **class in java. util while Collection is an interface.**
    - It has static methods for sorting, filerting etc
        - Collections.sort()
        - Collections.binarySearch()
        - Collections.shuffle()

### **What is the need of the Collections Framework?**

- If i want to declare 10k variables to overcome this problem we use arrays to counter it.
- Student s= new Student[10000];
    - **Advantages-**
        - We can represent a huge amount of values with the help of just one variable.
        - Readability of the code is improved.
    - **Limitations of Array:**
        - Finding an element is **O(N) Operation**.
        - Fixed size.
        - **Homogenous data** holding property-incompatible types found.
        - Readymade methods **support is not present in java for arrays**.
            - **Contains() method**
            - **addAll() method**
    - **How to counter homogeneous arrays?**
        - As the parent class can hold the child class objects.
        - Object[]a = new Object[10000];
        - a[0]= new Student();
        - a[1]= new customer();
## What are differences in Arrays and Collections?
- Arrays are fixed in size while collections are growable.
- Arrays performance is better, while collections is lower.
- Array can store homogenous elements,collections=> heterogenous.
- Arrays primitives and objects allowed, collections=> Only objects are allowed
- Arrays are less API Dependent, collections are more API dependent.
