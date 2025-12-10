# Constructors in C++

## What is a Constructor?

A **constructor** is a special member function of a class that is automatically called when an object of that class is created. It has the same name as the class and no return type (not even void).

**Primary Purpose:**
- Initialize the object's data members
- Allocate resources (memory, file handles, etc.)
- Set up the object's initial state
- Perform any setup operations needed before the object is used

## Key Characteristics of Constructors

1. **Same name as the class**
2. **No return type** (not even void)
3. **Automatically called** when an object is created
4. **Can be overloaded** (multiple constructors with different parameters)
5. **Cannot be virtual**
6. **Cannot be static**
7. **Can have access specifiers** (public, private, protected)

## Types of Constructors

### 1. Default Constructor

A constructor that takes **no parameters** or has all parameters with default values.

```cpp
class Student {
private:
    string name;
    int age;
    
public:
    // Default constructor
    Student() {
        name = "Unknown";
        age = 0;
        cout << "Default constructor called" << endl;
    }
};

// Usage
Student s1;  // Calls default constructor
```

**Important Notes:**
- If you don't define any constructor, C++ provides a default constructor automatically
- Once you define ANY constructor, the compiler-provided default constructor is no longer available
- The compiler-generated default constructor does nothing except allocate memory

### 2. Parameterized Constructor

A constructor that takes **one or more parameters** to initialize objects with specific values.

```cpp
class Student {
private:
    string name;
    int age;
    int rollNumber;
    
public:
    // Parameterized constructor
    Student(string n, int a, int roll) {
        name = n;
        age = a;
        rollNumber = roll;
        cout << "Parameterized constructor called" << endl;
    }
};

// Usage
Student s1("Alice", 20, 101);  // Calls parameterized constructor
```

### 3. Copy Constructor

A constructor that creates a new object as a **copy of an existing object**.

```cpp
class Student {
private:
    string name;
    int age;
    
public:
    // Parameterized constructor
    Student(string n, int a) {
        name = n;
        age = a;
    }
    
    // Copy constructor
    Student(const Student &s) {
        name = s.name;
        age = s.age;
        cout << "Copy constructor called" << endl;
    }
    
    void display() {
        cout << "Name: " << name << ", Age: " << age << endl;
    }
};

// Usage
Student s1("Bob", 21);
Student s2 = s1;  // Calls copy constructor
Student s3(s1);   // Also calls copy constructor
```

**When Copy Constructor is Called:**
- When an object is initialized with another object of the same class
- When an object is passed by value to a function
- When an object is returned by value from a function

**Default Copy Constructor:**
- If you don't define a copy constructor, C++ provides one automatically
- It performs a **shallow copy** (member-by-member copy)
- For classes with pointers or dynamic memory, you should define your own copy constructor for **deep copy**

### 4. Move Constructor (C++11 and later)

A constructor that **transfers ownership** of resources from a temporary object.

```cpp
class Array {
private:
    int* data;
    int size;
    
public:
    // Move constructor
    Array(Array&& other) noexcept {
        data = other.data;
        size = other.size;
        
        other.data = nullptr;
        other.size = 0;
        
        cout << "Move constructor called" << endl;
    }
};
```

### 5. Delegating Constructor (C++11 and later)

A constructor that **calls another constructor** of the same class.

```cpp
class Student {
private:
    string name;
    int age;
    int rollNumber;
    
public:
    // Constructor 1
    Student(string n, int a, int roll) {
        name = n;
        age = a;
        rollNumber = roll;
    }
    
    // Constructor 2 delegates to Constructor 1
    Student(string n) : Student(n, 0, 0) {
        cout << "Delegating constructor called" << endl;
    }
};
```

## Constructor Initialization List

A more efficient way to initialize member variables, especially for const members, references, and objects without default constructors.

**Syntax:**
```cpp
ClassName(parameters) : member1(value1), member2(value2) {
    // Constructor body
}
```

**Example:**
```cpp
class Student {
private:
    string name;
    int age;
    const int rollNumber;  // const member must be initialized
    
public:
    // Using initialization list
    Student(string n, int a, int roll) : name(n), age(a), rollNumber(roll) {
        cout << "Constructor with initialization list" << endl;
    }
};
```

**Benefits of Initialization List:**
- **More efficient**: Direct initialization instead of assignment
- **Required for**: const members, reference members, members without default constructors
- **Better performance**: Avoids creating temporary objects
- **Initialization order**: Members are initialized in declaration order, not list order

## Complete Practical Example
**Show:**
<details> <summary>Show</summary>

```cpp
#include <iostream>
#include <string>
#include <cstring>
using namespace std;

// Example 1: Basic Constructor Types
class Student {
private:
    string name;
    int age;
    int rollNumber;
    
public:
    // 1. Default Constructor
    Student() {
        name = "Unknown";
        age = 0;
        rollNumber = 0;
        cout << "Default constructor called" << endl;
    }
    
    // 2. Parameterized Constructor
    Student(string n, int a, int roll) {
        name = n;
        age = a;
        rollNumber = roll;
        cout << "Parameterized constructor called for " << name << endl;
    }
    
    // 3. Copy Constructor
    Student(const Student &s) {
        name = s.name;
        age = s.age;
        rollNumber = s.rollNumber;
        cout << "Copy constructor called for " << name << endl;
    }
    
    void display() {
        cout << "Name: " << name << ", Age: " << age 
             << ", Roll: " << rollNumber << endl;
    }
};

// Example 2: Constructor with Initialization List
class Rectangle {
private:
    double length;
    double width;
    const int id;  // const member
    
public:
    // Constructor using initialization list
    Rectangle(double l, double w, int i) : length(l), width(w), id(i) {
        cout << "Rectangle " << id << " created with initialization list" << endl;
    }
    
    double area() {
        return length * width;
    }
    
    void display() {
        cout << "Rectangle ID: " << id << ", Area: " << area() << endl;
    }
};

// Example 3: Constructor Overloading
class BankAccount {
private:
    string accountHolder;
    int accountNumber;
    double balance;
    
public:
    // Constructor 1: No parameters
    BankAccount() {
        accountHolder = "Anonymous";
        accountNumber = 0;
        balance = 0.0;
        cout << "Account created with default values" << endl;
    }
    
    // Constructor 2: Name only
    BankAccount(string name) {
        accountHolder = name;
        accountNumber = 1000;
        balance = 0.0;
        cout << "Account created for " << name << " with default balance" << endl;
    }
    
    // Constructor 3: Name and balance
    BankAccount(string name, double bal) {
        accountHolder = name;
        accountNumber = 1000;
        balance = bal;
        cout << "Account created for " << name << " with balance $" << bal << endl;
    }
    
    // Constructor 4: All parameters
    BankAccount(string name, int accNum, double bal) {
        accountHolder = name;
        accountNumber = accNum;
        balance = bal;
        cout << "Full account created for " << name << endl;
    }
    
    void display() {
        cout << "Holder: " << accountHolder << ", Account: " << accountNumber 
             << ", Balance: $" << balance << endl;
    }
};

// Example 4: Deep Copy Constructor (for dynamic memory)
class DynamicArray {
private:
    int* data;
    int size;
    
public:
    // Constructor
    DynamicArray(int s) {
        size = s;
        data = new int[size];
        for (int i = 0; i < size; i++) {
            data[i] = i + 1;
        }
        cout << "Array of size " << size << " created" << endl;
    }
    
    // Deep Copy Constructor
    DynamicArray(const DynamicArray &arr) {
        size = arr.size;
        data = new int[size];  // Allocate new memory
        for (int i = 0; i < size; i++) {
            data[i] = arr.data[i];  // Copy values
        }
        cout << "Deep copy constructor called" << endl;
    }
    
    // Destructor
    ~DynamicArray() {
        delete[] data;
        cout << "Array destroyed" << endl;
    }
    
    void display() {
        cout << "Array elements: ";
        for (int i = 0; i < size; i++) {
            cout << data[i] << " ";
        }
        cout << endl;
    }
    
    void modify(int index, int value) {
        if (index >= 0 && index < size) {
            data[index] = value;
        }
    }
};

// Example 5: Delegating Constructor
class Employee {
private:
    string name;
    int empID;
    double salary;
    string department;
    
public:
    // Main constructor
    Employee(string n, int id, double sal, string dept) {
        name = n;
        empID = id;
        salary = sal;
        department = dept;
        cout << "Main constructor: Employee " << name << " created" << endl;
    }
    
    // Delegating constructor 1
    Employee(string n, int id) : Employee(n, id, 50000.0, "General") {
        cout << "Delegating constructor 1 used" << endl;
    }
    
    // Delegating constructor 2
    Employee(string n) : Employee(n, 0, 30000.0, "Intern") {
        cout << "Delegating constructor 2 used" << endl;
    }
    
    void display() {
        cout << "Name: " << name << ", ID: " << empID 
             << ", Salary: $" << salary << ", Dept: " << department << endl;
    }
};

// Example 6: Private Constructor (Singleton Pattern)
class Singleton {
private:
    static Singleton* instance;
    int value;
    
    // Private constructor
    Singleton(int v) {
        value = v;
        cout << "Singleton instance created" << endl;
    }
    
public:
    // Static method to get instance
    static Singleton* getInstance(int v = 0) {
        if (instance == nullptr) {
            instance = new Singleton(v);
        }
        return instance;
    }
    
    void display() {
        cout << "Singleton value: " << value << endl;
    }
};

// Initialize static member
Singleton* Singleton::instance = nullptr;

int main() {
    cout << "========== EXAMPLE 1: BASIC CONSTRUCTORS ==========" << endl;
    Student s1;                              // Default
    Student s2("Alice", 20, 101);           // Parameterized
    Student s3 = s2;                        // Copy
    Student s4(s2);                         // Copy (alternate syntax)
    
    s1.display();
    s2.display();
    s3.display();
    
    cout << "\n========== EXAMPLE 2: INITIALIZATION LIST ==========" << endl;
    Rectangle r1(5.0, 3.0, 1);
    Rectangle r2(7.5, 4.2, 2);
    r1.display();
    r2.display();
    
    cout << "\n========== EXAMPLE 3: CONSTRUCTOR OVERLOADING ==========" << endl;
    BankAccount acc1;
    BankAccount acc2("John Doe");
    BankAccount acc3("Jane Smith", 5000.0);
    BankAccount acc4("Bob Johnson", 2001, 10000.0);
    
    acc1.display();
    acc2.display();
    acc3.display();
    acc4.display();
    
    cout << "\n========== EXAMPLE 4: DEEP COPY ==========" << endl;
    DynamicArray arr1(5);
    arr1.display();
    
    DynamicArray arr2 = arr1;  // Deep copy
    arr2.display();
    
    cout << "Modifying arr2..." << endl;
    arr2.modify(0, 999);
    
    cout << "After modification:" << endl;
    arr1.display();  // Should remain unchanged
    arr2.display();  // Should show modified value
    
    cout << "\n========== EXAMPLE 5: DELEGATING CONSTRUCTOR ==========" << endl;
    Employee emp1("Alice Johnson", 101, 75000.0, "Engineering");
    Employee emp2("Bob Smith", 102);
    Employee emp3("Charlie Brown");
    
    emp1.display();
    emp2.display();
    emp3.display();
    
    cout << "\n========== EXAMPLE 6: SINGLETON PATTERN ==========" << endl;
    Singleton* s = Singleton::getInstance(42);
    s->display();
    
    Singleton* s_again = Singleton::getInstance(100);  // Won't create new instance
    s_again->display();  // Shows same value (42)
    
    cout << "\n========== PROGRAM END ==========" << endl;
    
    return 0;
}
```

</details>

## Constructor vs Destructor

| Feature | Constructor | Destructor |
|---------|-------------|------------|
| Name | Same as class name | Same as class name with `~` prefix |
| Return Type | No return type | No return type |
| Parameters | Can have parameters | No parameters |
| Overloading | Can be overloaded | Cannot be overloaded |
| Called | When object is created | When object is destroyed |
| Purpose | Initialize object | Clean up resources |

## Special Cases and Advanced Topics

### 1. Explicit Constructor

Prevents implicit type conversions:

```cpp
class Integer {
private:
    int value;
    
public:
    explicit Integer(int v) {
        value = v;
    }
};

// Usage
Integer i1(10);      // OK
Integer i2 = 20;     // Error: implicit conversion prevented
```

### 2. Default Constructor with Default Arguments

```cpp
class Point {
private:
    int x, y;
    
public:
    Point(int xCoord = 0, int yCoord = 0) {
        x = xCoord;
        y = yCoord;
    }
};

// Can be called as:
Point p1;           // Uses defaults: (0, 0)
Point p2(5);        // (5, 0)
Point p3(5, 10);    // (5, 10)
```

### 3. Constructor in Inheritance

```cpp
class Base {
public:
    Base() {
        cout << "Base constructor" << endl;
    }
};

class Derived : public Base {
public:
    Derived() {
        cout << "Derived constructor" << endl;
    }
};

// Output when creating Derived object:
// Base constructor
// Derived constructor
```

## Common Constructor Mistakes

### 1. Forgetting to Initialize Members

```cpp
// BAD
class Student {
    string name;
    int age;
public:
    Student(string n) {
        name = n;
        // age left uninitialized!
    }
};

// GOOD
class Student {
    string name;
    int age;
public:
    Student(string n) : name(n), age(0) {
        // All members initialized
    }
};
```

### 2. Shallow Copy Problem

```cpp
// BAD - Default copy constructor does shallow copy
class Array {
    int* data;
public:
    Array(int size) {
        data = new int[size];
    }
    // No copy constructor defined!
    // Default copy copies pointer, not data
};

// GOOD - Define deep copy constructor
class Array {
    int* data;
    int size;
public:
    Array(int s) {
        size = s;
        data = new int[size];
    }
    
    Array(const Array& other) {
        size = other.size;
        data = new int[size];
        for (int i = 0; i < size; i++) {
            data[i] = other.data[i];
        }
    }
};
```

### 3. Not Using Initialization List for const/Reference Members

```cpp
// ERROR - Won't compile
class MyClass {
    const int id;
public:
    MyClass(int i) {
        id = i;  // ERROR: can't assign to const
    }
};

// CORRECT
class MyClass {
    const int id;
public:
    MyClass(int i) : id(i) {
        // Initialization list required for const
    }
};
```

## Constructor Summary

1. **Always initialize all member variables** - Uninitialized members lead to undefined behavior
2. **Use initialization lists** - More efficient, especially for complex objects
3. **Provide a default constructor** when appropriate - Makes your class easier to use
4. **Define copy constructor for classes with pointers** - Prevents shallow copy issues
5. **Use explicit keyword** - Prevents unintended implicit conversions
6. **Keep constructors simple** - Complex logic should be in separate methods
7. **Validate parameters** - Check input values for validity
8. **Document what each constructor does** - Makes code maintainable

## When to Use Which Constructor?

| Situation | Constructor Type |
|-----------|-----------------|
| Creating object with no specific values | Default Constructor |
| Creating object with specific initial values | Parameterized Constructor |
| Creating copy of existing object | Copy Constructor |
| Multiple ways to initialize an object | Constructor Overloading |
| Need to initialize const or reference members | Initialization List |
| Avoiding code duplication between constructors | Delegating Constructor |
| Working with temporary objects (optimization) | Move Constructor |

