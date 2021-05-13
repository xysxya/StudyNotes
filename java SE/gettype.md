```
package temp;


//Java program to demonstrate getType() method

import java.lang.reflect.Field;

public class GFG {

 public static void main(String[] args)
     throws Exception
 {

     // Get the marks field object
     Field field = User.class.getField("Marks");

     // Apply getType Method on User Object
     // to get the Type of Marks field
     Class value = field.getType();

     // print result
     System.out.println("Type"
                        + " is " + value);

     // Now Get the Fees field object
     field = User.class.getField("Fees");

     // Apply getType Method on User Object
     // to get the Type of Fees field
     value = field.getType();

     // print result
     System.out.println("Type"
                        + " is " + value);
 }
}

//sample User class
class User {

 // static double values
 public static double Marks = 34.13;
 public static float Fees = 3413.99f;

 public static double getMarks()
 {
     return Marks;
 }

 public static void setMarks(double marks)
 {
     Marks = marks;
 }

 public static float getFees()
 {
     return Fees;
 }

 public static void setFees(float fees)
 {
     Fees = fees;
 }
}
```
