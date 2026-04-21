Looks like you’re listing core Java I/O concepts—good foundation stuff. Let’s connect them clearly so you actually understand how they fit together (not just memorize them).

### 📁 1. File Class
- The File class (in java.io) is used to represent a file or directory, not to read/write data.
- 👉 Think of it as: “file metadata handler”
Example:
```
import java.io.File;
public class Main {    
    public static void main(String[] args) {       
        File file = new File("example.txt");       
        System.out.println(file.exists());      
        System.out.println(file.getName());     
        System.out.println(file.getAbsolutePath());
    }   
      
}

```

### 📖 2. FileReader
- Used to read character data from a file.
- Best for text files.

```
import java.io.FileReader;

FileReader fr = new FileReader("example.txt");
int ch;
while ((ch = fr.read()) != -1) {    
    System.out.print((char) ch);
}
fr.close();
```

### ✍️ 3. FileWriter
Used to write character data to a file.
```
import java.io.FileWriter;
FileWriter fw = new FileWriter("example.txt");
fw.write("Hello World");
fw.close();


```
👉 By default, it overwrites the file.
To append:
FileWriter fw = new FileWriter("example.txt", true);

### ⚡ 4. BufferedReader
Wraps FileReader to make reading faster and easier (especially line-by-line).

```
import java.io.*;
BufferedReader br = new BufferedReader(new FileReader("example.txt"));
String line;
while ((line = br.readLine()) != null) {    
    System.out.println(line);
}
br.close();

```
#### 👉 Why use it?

- Faster (uses buffer)
- Has readLine() (very useful)

### ⚡ 5. BufferedWriter
Wraps FileWriter for efficient writing.

```
import java.io.*;
BufferedWriter bw = new BufferedWriter(new FileWriter("example.txt"));
bw.write("Hello Buffered Writer");
bw.newLine();
bw.close();
```

### 🔐 6. Serialization

- Process of converting an object into a byte stream (so you can save it to file or send over network).

- 👉 Class must implement Serializable.

```
import java.io.*;

class Student implements Serializable {   
     int id;    
     String name;   

     Student(int id, String name) {     
        this.id = id;        
        this.name = name;    
    }
} 

    public class Main {
        public static void main(String[] args) throws Exception {
            Student s1 = new Student(101, "Saravanan");

            FileOutputStream file = new FileOutputStream("data.txt");
            ObjectOutputStream out = new ObjectOutputStream(file);

            out.writeObject(s1);
            out.close();
            file.close();

            System.out.println("Object serialized and saved to file");
        }
}
```

### 🔓 7. Deserialization
- Reverse process: reading object from file.

```
FileInputStream file = new FileInputStream("data.txt");
ObjectInputStream in = new ObjectInputStream(file);

Student s = (Student) in.readObject();

System.out.println(s.id + " " + s.name);

in.close();
file.close();

```

#### 🧠 How everything connects



- BufferedReader/BufferedWriter     → faster + convenient
- Serialization → store objects
- Deserialization → retrieve objects



#### 💡 Real-world tip

In modern Java, people often prefer:


- Files (NIO package)
- Paths
- try-with-resources


#### Example:

```
try (BufferedReader br = new BufferedReader(new FileReader("example.txt"))) {    
    System.out.println(br.readLine());
}

``



