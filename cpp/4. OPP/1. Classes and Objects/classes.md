# Classes and Objects in C++

Classes and objects are fundamental to Object-Oriented Programming (OOP) in C++.

## What is a Class?

A **class** is a user-defined data type that serves as a blueprint or template for creating objects. It encapsulates data (attributes) and functions (methods) that operate on that data into a single unit.

Think of a class like an architectural blueprint for a house—it defines what the house will contain and how it will function, but it's not the actual house itself.

## What is an Object?

An **object** is an instance of a class. It's the actual entity created in memory based on the class blueprint. If a class is the blueprint, an object is the house built from that blueprint.

## Basic Syntax

```cpp
class ClassName {
    // Access specifier
    private:
        // Private members (data and functions)
        
    public:
        // Public members (data and functions)
        
    protected:
        // Protected members (data and functions)
};

// Creating object (instances of the class)
ClassName object1;
```

## Access Specifiers

C++ provides three access specifiers that control how class members can be accessed:

**1. Private:** Members are accessible only within the class itself. This is the default access level for class members.

**2. Public:** Members are accessible from anywhere in the program where the object is visible.

**3. Protected:** Members are accessible within the class and by derived classes (used in inheritance).

### 1. Public Access Specifier
```cpp
#include <iostream>
#include <string>
using namespace std;

class Student
{
public:
    // Public data members
    string name;
    int age;
    int rollNumber;

    // Regular member function
    void displayInfo()
    {
        cout << "Name: " << name << endl;
        cout << "Age: " << age << endl;
        cout << "Roll Number: " << rollNumber << endl;
    }
};

int main()
{
    // Creating objects (instances of the class)
    Student student1; // Using default constructor

    // Accessing public data members
    student1.name = "Ali";
    student1.age = 21;
    student1.rollNumber = 9999;

    cout << "Student 1 Information:" << endl;
    // Accessing public methods
    student1.displayInfo();

    return 0;
}
```

### 2. Protected Access Specifier
```cpp
#include <iostream>
#include <string>
using namespace std;

class Student
{
protected:
    // Protected data members
    string name;
    int age;
    int rollNumber;

public:
    // Regular member function
    void displayInfo()
    {
        cout << "Name: " << name << endl;
        cout << "Age: " << age << endl;
        cout << "Roll Number: " << rollNumber << endl;
    }
};

int main()
{
    // Creating objects (instances of the class)
    Student student1; // Using default constructor

    // Accessing protected data members
    student1.name = "Ali";      // error: 'std::string Student::name' is protected within this contex
    student1.age = 21;          // error: 'int Student::age' is protected within this context
    student1.rollNumber = 9999; // error: 'int Student::rollNumber' is protected within this context

    cout << "Student 1 Information:" << endl;
    // Accessing public methods
    student1.displayInfo();

    return 0;
}
```

### 3. Private Access Specifier
```cpp
#include <iostream>
#include <string>
using namespace std;

class Student
{
private:
    // Private data members
    string name;
    int age;
    int rollNumber;

public:
    // Regular member function
    void displayInfo()
    {
        cout << "Name: " << name << endl;
        cout << "Age: " << age << endl;
        cout << "Roll Number: " << rollNumber << endl;
    }
};

int main()
{
    // Creating objects (instances of the class)
    Student student1; // Using default constructor

    // Accessing private data members
    student1.name = "Ali";      // error: 'std::string Student::name' is private within this context
    student1.age = 21;          // error: 'int Student::age' is private within this context
    student1.rollNumber = 9999; // error: 'int Student::rollNumber' is private within this context

    cout << "Student 1 Information:" << endl;
    // Accessing public methods
    student1.displayInfo();

    return 0;
}
```

## Complete Example

```cpp
#include <iostream>
#include <string>
using namespace std;

class Student {
private:
    // Private data members
    string name;
    int age;
    int rollNumber;
    float gpa;

public:
    // Constructor - special function called when object is created
    Student() {
        name = "Unknown";
        age = 0;
        rollNumber = 0;
        gpa = 0.0;
    }
    
    // Parameterized constructor
    Student(string n, int a, int roll, float g) {
        name = n;
        age = a;
        rollNumber = roll;
        gpa = g;
    }
    
    // Setter methods (mutators)
    void setName(string n) {
        name = n;
    }
    
    void setAge(int a) {
        if (a > 0) {
            age = a;
        }
    }
    
    void setRollNumber(int roll) {
        rollNumber = roll;
    }
    
    void setGPA(float g) {
        if (g >= 0.0 && g <= 4.0) {
            gpa = g;
        }
    }
    
    // Getter methods (accessors)
    string getName() {
        return name;
    }
    
    int getAge() {
        return age;
    }
    
    int getRollNumber() {
        return rollNumber;
    }
    
    float getGPA() {
        return gpa;
    }
    
    // Regular member function
    void displayInfo() {
        cout << "Name: " << name << endl;
        cout << "Age: " << age << endl;
        cout << "Roll Number: " << rollNumber << endl;
        cout << "GPA: " << gpa << endl;
    }
    
    // Destructor - called when object is destroyed
    ~Student() {
        cout << "Student object destroyed" << endl;
    }
};

int main() {
    // Creating objects (instances of the class)
    Student student1; // Using default constructor
    Student student2("Emad", 20, 101, 3.8); // Using parameterized constructor
    
    // Accessing public methods
    student1.setName("Ali");
    student1.setAge(21);
    student1.setRollNumber(102);
    student1.setGPA(3.5);
    
    cout << "Student 1 Information:" << endl;
    student1.displayInfo();
    
    cout << "\nStudent 2 Information:" << endl;
    student2.displayInfo();
    
    return 0;
}
```

## Main Concepts

### 1. Constructors

Constructors are special member functions that are automatically called when an object is created. They have the same name as the class and no return type.

**Types of constructors:**
- **Default constructor:** Takes no parameters
- **Parameterized constructor:** Takes parameters to initialize object with specific values
- **Copy constructor:** Creates a new object as a copy of an existing object

### 2. Destructors

A destructor is a special member function called automatically when an object goes out of scope or is explicitly deleted. It has the same name as the class preceded by a tilde (~) and takes no parameters.

### 3. Encapsulation

This is the principle of bundling data and methods that work on that data within a class, and restricting direct access to some components. Private data members can only be accessed through public methods (getters and setters), providing controlled access.

### 4. Data Hiding

By making data members private, we hide the internal implementation details from outside access. This protects data from accidental modification and maintains the integrity of the object's state.

## Memory Allocation for Objects

When you create an object, memory is allocated for all its data members. Member functions are typically stored separately and shared among all objects of the class.

```cpp
// Object created on the stack
Student s1;

// Object created on the heap (dynamic allocation)
Student* s2 = new Student("Ahmed", 22, 103, 3.9);
delete s2; // Must manually free memory
```

## The 'this' Pointer

Every object has access to its own address through a pointer called `this`. It's useful when you need to refer to the calling object itself.

```cpp
class Student {
private:
    string name;
public:
    void setName(string name) {
        this->name = name; // Differentiates between parameter and member
    }
};
```

## Static Members

**Static data members** are shared among all objects of the class. Only one copy exists regardless of how many objects are created.

**Static member functions** can be called without creating an object and can only access static members.

```cpp
class Counter {
private:
    static int count; // Static data member
    
public:
    Counter() {
        count++;
    }
    
    static int getCount() { // Static member function
        return count;
    }
};

// Static member must be defined outside class
int Counter::count = 0;
```

