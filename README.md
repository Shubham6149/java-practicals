# java-practicals
# SHUBHAM VERMA
# ROLL.NO:- 24107060

# Q1  Design a class Complex having a real part (x) and an imaginary part (y). Provide methods to perform the following on complex numbers: 
# a. Add and Multiply two complex numbers. 
# b. toString() method to display complex numbers in the form: x + i y 
# CODE
```
public class complex {
    private double x; 
    private double y; 

    
    public complex(double x, double y) {
        this.x = x;
        this.y = y;
    }

    
    public complex add(complex other) {
        return new complex(this.x + other.x, this.y + other.y);
    }

    
    public complex multiply(complex other) {
        double real = (this.x * other.x) - (this.y * other.y);
        double imaginary = (this.x * other.y) + (this.y * other.x);
        return new complex(real, imaginary);
    }

    
    @Override
    public String toString() {
        return x + " + i" + y;
    }

    
    public static void main(String[] args) {
        complex c1 = new complex(9, 6);
        complex c2 = new complex(8, 3);

        complex sum = c1.add(c2);
        complex product = c1.multiply(c2);

        System.out.println("First Complex Number: " + c1);
        System.out.println("Second Complex Number: " + c2);
        System.out.println("Sum: " + sum);
        System.out.println("Product: " + product);
    }
}
```

# OUTPUT
![image alt](https://github.com/Shubham6149/java-practicals/blob/87f1bd3a4ddfe772a92dc377a53c69957485a45b/Screenshot%202025-05-21%20141605.png)


# Q2  Create a class TwoDim which contains private members as x and y coordinates in package P1. Define the default constructor, a parameterized constructor and override toString() method to display the co ordinates. Now reuse this class and in package P2 create another class ThreeDim, adding a new dimension as z as its private member.  Define the constructors for the subclass and override toString() method in the subclass also. Write appropriate methods to show dynamic method dispatch. The main() function should be in a package P. 

# code
```
package P1;

public class TwoDim {
    private int x, y;
//d constructor
    public TwoDim() {
        this.x = 0;
        this.y = 0;
    }
//p constructor
    public TwoDim(int x, int y) {
        this.x = x;
        this.y = y;
    }

    public String toString() {
        return "Coordinates: x = " + x + ", y = " + y;
    }
}
```

```
package P2;

import P1.TwoDim;

public class ThreeDim extends TwoDim {
    private int z;

    public ThreeDim() {
        super();
        this.z = 0;
    }

    public ThreeDim(int x, int y, int z) {
        super(x, y);
        this.z = z;
    }

    @Override
    public String toString() {
        return super.toString() + ", z = " + z;
    }
}
```

```
package P;

import P1.TwoDim;
import P2.ThreeDim;

public class Main {
    public static void main(String[] args) {
        TwoDim obj;

        obj = new TwoDim(1, 2);
        System.out.println("TwoDim object: " + obj.toString());

        obj = new ThreeDim(3, 4, 5); // Dynamic Method Dispatch
        System.out.println("ThreeDim object (via TwoDim reference): " + obj.toString());
    }
}
```
# output
![image alt](https://github.com/Shubham6149/java-practicals/blob/43257d07950e945253d3dc165c9b7aaa60326dba/Screenshot%202025-05-21%20142020.png)


# Q3  Define an abstract class Shape in package P1. Inherit two more classes: Rectangle in package P2 and Circle in package P3. Write a program to ask the user for the type of shape and then using the concept of dynamic method dispatch, display the area of the appropriate subclass. Also write appropriate methods to read the data. The main() function should not be in any package. 

# code
```
package Q1;

public abstract class Shape {
    public abstract void read();
    public abstract void area();
}
```

```
package Q2;

import java.util.Scanner;
import Q1.Shape;

public class Rectangle extends Shape {
    double length, breadth;

    public void read() {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter length of rectangle: ");
        length = sc.nextDouble();
        System.out.print("Enter breadth of rectangle: ");
        breadth = sc.nextDouble();
    }

    public void area() {
        System.out.println("Area of Rectangle: " + (length * breadth));
    }
}
```

```
package Q3;

import java.util.Scanner;
import Q1.Shape;

public class Circle extends Shape {
    double radius;

    public void read() {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter radius of circle: ");
        radius = sc.nextDouble();
    }

    public void area() {
        System.out.println("Area of Circle: " + (Math.PI * radius * radius));
    }
}
```

```
import Q1.Shape;
import Q2.Rectangle;
import Q3.Circle;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        Shape shape;

        System.out.print("Enter type of shape (rectangle/circle): ");
        String type = sc.nextLine().toLowerCase();

        switch (type) {
            case "rectangle":
                shape = new Rectangle();
                break;
            case "circle":
                shape = new Circle();
                break;
            default:
                System.out.println("Invalid shape type.");
                return;
        }

        shape.read(); // dynamic method dispatch
        shape.area(); // dynamic method dispatch
    }
}
```

# output
![image alt](https://github.com/Shubham6149/java-practicals/blob/a97569fa6ff7abe7f9c4f4f48f697ae2a82933b7/Screenshot%202025-05-21%20144350.png)

# Q4 Create an exception subclass UnderAge, which prints “Under Age” along with the age value when an object of UnderAge class is printed in the catch statement. Write a class exceptionDemo in which the method test() throws UnderAge exception if the variable age passed to it as argument is less than 18. Write main() method also to show working of the program.  

# code
```
public class ExceptionDemo {

    
    static class UnderAge extends Exception {
        private int age;

        public UnderAge(int age) {
            this.age = age;
        }

        @Override
        public String toString() {
            return "Under Age: " + age;
        }
    }


    public void test(int age) throws UnderAge {
        if (age < 18) {
            throw new UnderAge(age);
        } else {
            System.out.println("Age is valid: " + age);
        }
    }
```

# output 
![image alt](https://github.com/Shubham6149/java-practicals/blob/b3b240524a2713bfb5ba4aa5cd13e093894346bc/Screenshot%202025-05-21%20142310.png)

# Q6  Write a program that copies content of one file to another. Pass the names of the files through command-line arguments.

# code
```
import java.io.*;

public class FileCopy {
    public static void main(String[] args) {
        
        if (args.length != 2) {
            System.out.println("Usage: java FileCopy <source_file> <destination_file>");
            return;
        }

        String sourceFile = args[0];
        String destFile = args[1];

        try (
            FileInputStream fis = new FileInputStream(sourceFile);
            FileOutputStream fos = new FileOutputStream(destFile);
        ) {
            int byteData;
            while ((byteData = fis.read()) != -1) {
                fos.write(byteData);
            }
            System.out.println("File copied successfully.");
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

![image alt](https://github.com/Shubham6149/java-practicals/blob/6658de08885a3ca4dd2796712d360c657f787b31/Screenshot%202025-05-21%20142655.png)

# ouput
![image alt]()


![image alt]()


# Q7 Write a program to read a file and display only those lines that have the first two characters as '//' (Use try with resources). 
```
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class DisplayCommentLines {
    public static void main(String[] args) {
        String filePath = "7.txt"; 

        try (BufferedReader reader = new BufferedReader(new FileReader(filePath))) {
            String line;

            while ((line = reader.readLine()) != null) {
                if (line.trim().startsWith("//")) {  // Added trim() to ignore leading spaces
                    System.out.println(line);
                }
            }
        } catch (IOException e) {
            System.out.println("An error occurred: " + e.getMessage());
        }
    }
}
```

![image alt]()

# output
![image alt]()



# Q9 Write a program to display a string in frame window with pink color as background. 

# code
```
import java.awt.*;

public class StringInFrame extends Frame {

    String message = "shubham verma";

    public StringInFrame() {

        setTitle("Pink Background Frame");

    
        setSize(400, 200);


        setBackground(Color.PINK);


        setVisible(true);
    }


    public void paint(Graphics g) {
        g.setColor(Color.BLACK); 
        g.setFont(new Font("Arial", Font.BOLD, 20));
        g.drawString(message, 50, 100);
    }


    public static void main(String[] args) {
        StringInFrame f = new StringInFrame();

        
        f.addWindowListener(new java.awt.event.WindowAdapter() {
            public void windowClosing(java.awt.event.WindowEvent e) {
                f.dispose();
            }
        });
    }
}
```

# output
![image alt]()

