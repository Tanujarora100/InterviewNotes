# **Input-Output Streams:**
- If we provide data to the Java applications and then that data is called input data and operation is called Input operation.
To Perform Input Operations we wil use set of instructions->Input Statements
- If we submit data from Java application then that data is called Output Data and Operation is called Output Operations.
- To Perform these I/O Operations -> Java Provided Streams to do it.
## **What is a Stream?**
- Stream is a channel or medium which allows input data to Java application and application to output devices.
## **How many types of streams are there in java?**
    - In General streams are classified into Two Ways:
        - Byte Oriented Streams
        - Character Oriented Streams

## **What are Byte Oriented Streams?**
- It is able to allow data in form of bytes to continue flow from input devices to java applications to output devices.
- The Length of the data item is of 1 byte.
- Two Types under this category:
    - Input Stream
        - It is able to allow data in from of bytes from input devices to java application.
        - EX: In java all streams are represented in form of predefined classes presented in [java.io](http://java.io) package
        - Types:
            - ByteArrayInputStream
            - FileInputStream
            - DataInputStream
            - ObjectInputStream
            - BufferedInputStream
    - Output Stream
        - These streams are able to allow data in form of  bytes from java application to Output devices.
        - Types:
            - ByteArrayOutputStream
            - FileOutputStream
            - DataOutputStream
            - ObjectOutputStream
            - BufferedOutputStream

## What is FileInputStream:
- implements autocloseable interface.


## **What are character Oriented Streams?**
- Allows data in the form of characters in continous flow from input devices to java applications and from java apps to output devices.
- In Character Oriented streams the length of the data item is of 2 Bytes
- There are 2 types of streams
    - Reader
        - Able to carry data in characters.
        - Examples:
            - CharArrayReader
            - FileReader
            - BufferedReader
            - InputStreamReader
    - Writer
        - Examples:
            - CharArrayWriter
            - FileWriter
            - PrintWriter
            - BufferedWriter
- All Character oriented Streams are ended with Reader or Writer and Byte One’s are ended with Stream.
- What is meant by file Operations?
    - To Get data and to set data to a particular target file.
    - Java provided 4 predefined stream classes:
        - Fileoutputstream
            - To send data from java application to a particular target file.
            - The second parameter of boolean is for appending or overwriting—>True means only append , False means Overwrite everything.
            - Throws IO Exception
            - They are implementing Autocloseable interface.
            - Good Practice:
                - Declare resources before try block.
                - Create the resources inside try block.
                - Close the resources inside finally block.
```java
package fileinputoutput;

import java.io.FileOutputStream;
import java.io.IOException;
import java.util.Arrays;
import java.util.List;

public class Reader {

    public static void main(String[] args) {
        String filePath = "C:\\Users\\colon\\Downloads\\FileReader.txt";
        String s = "Hello";
        List<String> strngArray = Arrays.asList("Hello", "TANUJ", "NEW ARRAY");
        FileOutputStream fos = null;
        try {

            fos = new FileOutputStream(filePath, false);
            fos.write(System.lineSeparator().getBytes());
            fos.write(s.getBytes());
            fos.write(System.lineSeparator().getBytes());

            for (String st : strngArray) {
                fos.write(st.getBytes());
                fos.write(System.lineSeparator().getBytes());
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                assert fos != null;
                fos.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
}
```
### FileInputStream
    - returns the information in bytes
    - we need to declare a byte array to read it.
### FileReader
```java
public class CopyAssignment {
    public static void main(String[] args) {
        CopyAssignment obj = new CopyAssignment();
        obj.copy();
    }

    private void copy() {
        String source = "C:\\Users\\colon\\Downloads\\New Text Document.txt";

        try (FileReader fr = new FileReader(source)) {
            StringBuilder sb = new StringBuilder();
            int charRead;
            while ((charRead=fr.read()) != -1) {
                sb.append((char) charRead);
            }
            System.out.println(sb.toString());
        } catch (IOException e) {
            e.printStackTrace();
        }

    }
}
```
### FileWriter
```java
public class Writer {
    public static void main(String[] args) {
        Writer obj = new Writer();
        obj.writeToFile();

    }

    public void writeToFile() {
        try (FileWriter fw = new FileWriter("C:\\Users\\colon\\Downloads\\FileReader.txt",true)) {
            String s = "Test";
            char[] c = s.toCharArray();
            //takes characters
            fw.write(System.lineSeparator());
            fw.write(c);
            fw.write(System.lineSeparator());


        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```
## Dynamic Input Approach

- If we provide data to java programs at Runtime then that data is called as Dynamic Input.
- To Perform dynamic input in java applications, it has provided 3 approaches
    - BufferedReader
    - Console
    - Scanner

## Buffered Reader Class:
- character based
- extends the reader class
- internal buffer of 8192 characters.

### Why it is useful?
- during the reading a chunk of characters is put into the buffer and read character by character then=> Less Read Operations=> more reading speed.

```java
import java.io.BufferedReader;
import java.io.FileInputStream;
import java.io.IOException;
import java.io.InputStreamReader;

public class Example {
    public static void main(String[] args) {
        try {
            FileInputStream fileInputStream = new FileInputStream("file.txt");
            InputStreamReader inputStreamReader = new InputStreamReader(fileInputStream);
            BufferedReader bufferedReader = new BufferedReader(inputStreamReader);

            String line;
            while ((line = bufferedReader.readLine()) != null) {
                // Process the line
                System.out.println(line);
            }

            // Close the BufferedReader when done
            bufferedReader.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

```
## Methods of BufferedReader:
- read()-> read single character
- read(char[] array)-> reads the character and store in array
- read(char[] array, int start, int length)=>reads the number of characters equal to length from the reader and stores in the specified array starting from the position start
- skip() method-> skip some characters
- mark()-> marks the position in reader up to which data has been read.

# File Class in Java?

## In Which Package it is located?
- java.io 

## What is a pathSeparator in File Class?
- To make the code more platform independent we can constant file.separator instead of '/' or '\'.

## Constructors in File Class
- File(File parent, String child)
    - here the parent is the parent directory or fiile which we create instance. It should be existent
    - child can be the path name or the new directory to which we create the object
```java
    File parentDirectory = new File("/path/to/parentDirectory");
String childFileName = "childFile.txt";

// Create a new File instance representing the child file within the parent directory
File childFile = new File(parentDirectory, childFileName);
```
## File Class Methods:
- canExecute()-> check if this file can be executed
- canRead()-> check if this file can be read.
- getParent()-> get the parent directory
- getParentFile()-> get the parent file
- getPath()-> get the path
- isFile()-> check if this file
- isHidden()
- listFiles-> File[]
- length()-> returns length in long.
- setExecutable()-> sets the permission to execute
- setReadable()-> sets the permission to read.

## java.io.Console
- added in JDK 1.6 Version
- character based.
