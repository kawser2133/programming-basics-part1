## **1. Classes and Objects in C#**

A **class** in C# is a blueprint or template for creating objects. It defines the structure of an object, including its properties (data), methods (behavior), and constructors (initialization logic). You can think of a class as a definition, while an object is an instance of that class, representing a specific entity.

#### Example:

```csharp
// Define a class named Car
public class Car
{
    // Fields (variables)
    private string make;
    private string model;

    // Constructor
    public Car(string make, string model)
    {
        this.make = make;
        this.model = model;
    }

    // Methods
    public void Drive()
    {
        Console.WriteLine($"{make} {model} is driving!");
    }
}

// Create an object of the Car class
Car car1 = new Car("Toyota", "Corolla");
car1.Drive();  // Output: Toyota Corolla is driving!
```

- **Class Definition**: The `Car` class is a blueprint that defines what a "car" looks like, including its `make`, `model`, and the ability to `Drive()`.
- **Object Creation**: The `car1` object is an instance of the `Car` class.

---

### **Fields, Properties, and Methods**

#### **Fields**
Fields are variables that hold data for the object. They are usually private and are accessed via **properties** to protect data integrity.

#### Example:
```csharp
public class Person
{
    // Field (Private variable)
    private string name;
    private int age;

    // Constructor to initialize fields
    public Person(string name, int age)
    {
        this.name = name;
        this.age = age;
    }
}
```

#### **Properties**
Properties in C# allow controlled access to fields. They are used to read and write field values through `get` and `set` accessors.

#### Example:
```csharp
public class Person
{
    // Field (Private variable)
    private string name;

    // Property to get and set the name
    public string Name
    {
        get { return name; }
        set { name = value; }
    }
}

Person person = new Person();
person.Name = "Alice";  // Set the name using property
Console.WriteLine(person.Name);  // Output: Alice
```
- **`get` Accessor**: Retrieves the value of the field.
- **`set` Accessor**: Assigns a new value to the field.

#### **Methods**
Methods define the actions or behaviors an object can perform. They can be public or private depending on whether they should be accessed from outside the class.

#### Example:
```csharp
public class Calculator
{
    // Method to add two numbers
    public int Add(int a, int b)
    {
        return a + b;
    }
}

// Using the method
Calculator calc = new Calculator();
int result = calc.Add(5, 10);
Console.WriteLine(result);  // Output: 15
```
---

### **Constructors**
A **constructor** is a special method that is automatically called when an object is created. It initializes the object’s state by assigning initial values to fields or properties.

#### Types of Constructors:
1. **Default Constructor**: No parameters.
2. **Parameterized Constructor**: Takes parameters to initialize fields.
3. **Static Constructor**: Initializes static members of a class.

#### Example of Parameterized Constructor:
```csharp
public class Book
{
    // Fields
    private string title;
    private string author;

    // Parameterized constructor
    public Book(string title, string author)
    {
        this.title = title;
        this.author = author;
    }

    // Method to display book details
    public void GetDetails()
    {
        Console.WriteLine($"Title: {title}, Author: {author}");
    }
}

// Create object using the constructor
Book book1 = new Book("1984", "George Orwell");
book1.GetDetails();  // Output: Title: 1984, Author: George Orwell
```

#### Default Constructor Example:
```csharp
public class Book
{
    private string title = "Unknown";

    // Default constructor
    public Book() { }

    public void GetTitle()
    {
        Console.WriteLine($"Title: {title}");
    }
}

Book book = new Book();
book.GetTitle();  // Output: Title: Unknown
```

#### **Static Constructor**:
A **static constructor** is used to initialize static members of a class. It is called once, before any instance of the class is created.

```csharp
public class MathHelper
{
    public static double Pi;

    // Static constructor
    static MathHelper()
    {
        Pi = 3.14159;
    }

    public static double CalculateCircleArea(double radius)
    {
        return Pi * radius * radius;
    }
}

// No need to create an instance
double area = MathHelper.CalculateCircleArea(5);
Console.WriteLine(area);  // Output: 78.53975
```
---

### **Types of Classes**

C# provides several types of classes, each with its specific use cases:

#### 1. **Static Classes**
A static class cannot be instantiated and is used to group related static methods and properties. All members of a static class must be static.

#### Example:
```csharp
public static class MathHelper
{
    public static double Pi = 3.14159;

    public static double CalculateCircleArea(double radius)
    {
        return Pi * radius * radius;
    }
}

// Usage without instantiation
double area = MathHelper.CalculateCircleArea(5);
Console.WriteLine(area);  // Output: 78.53975
```

- **Note**: You cannot create an object of a static class: `MathHelper helper = new MathHelper();` would result in an error.

#### 2. **Partial Classes**
Partial classes allow splitting the definition of a class across multiple files. This is useful when working on large projects with many developers.

#### Example:
```csharp
// File: Car_Part1.cs
public partial class Car
{
    public string Make { get; set; }
}

// File: Car_Part2.cs
public partial class Car
{
    public string Model { get; set; }

    public void DisplayDetails()
    {
        Console.WriteLine($"{Make} {Model}");
    }
}

// Both files together define a complete Car class
Car car = new Car();
car.Make = "Toyota";
car.Model = "Corolla";
car.DisplayDetails();  // Output: Toyota Corolla
```

#### 3. **Sealed Classes**
A sealed class cannot be inherited. It is used when you want to prevent other classes from deriving from it.

#### Example:
```csharp
public sealed class FinalClass
{
    public void Display()
    {
        Console.WriteLine("This class cannot be inherited.");
    }
}

// Error: You cannot inherit from a sealed class
// public class DerivedClass : FinalClass { }
```

#### 4. **Abstract Classes**
An abstract class cannot be instantiated directly and may contain abstract methods (without implementation) that must be implemented by derived classes. It can also contain fully implemented methods.

#### Example:
```csharp
public abstract class Animal
{
    // Abstract method (no implementation)
    public abstract void MakeSound();

    // Concrete method
    public void Sleep()
    {
        Console.WriteLine("The animal is sleeping.");
    }
}

public class Dog : Animal
{
    // Providing implementation for the abstract method
    public override void MakeSound()
    {
        Console.WriteLine("Dog barks.");
    }
}

Dog dog = new Dog();
dog.MakeSound();  // Output: Dog barks.
dog.Sleep();      // Output: The animal is sleeping.
```

#### 5. **Nested Classes**
A class declared inside another class is called a nested class. It is used when the relationship between the two classes is very close.

#### Example:
```csharp
public class OuterClass
{
    public class NestedClass
    {
        public void ShowMessage()
        {
            Console.WriteLine("This is a nested class.");
        }
    }
}

// Usage
OuterClass.NestedClass nested = new OuterClass.NestedClass();
nested.ShowMessage();  // Output: This is a nested class.
```

---

## **Summary**
- **Classes** are blueprints for creating objects.
- **Fields** store data, **properties** provide controlled access to fields, and **methods** define behavior.
- **Constructors** initialize the object’s state, and there are different types like default, parameterized, and static constructors.
- C# supports various **types of classes**:
  - **Static** classes provide only static members.
  - **Partial** classes allow class definitions across multiple files.
  - **Sealed** classes prevent inheritance.
  - **Abstract** classes define common functionality while enforcing subclasses to implement certain methods.
  - **Nested** classes allow close class relationships.

