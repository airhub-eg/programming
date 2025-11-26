# Object-Oriented Programming in C++

Object-Oriented Programming (OOP) is a programming paradigm that organizes software design around objects and data rather than functions and logic. C++ is a powerful language that fully supports OOP principles, making it ideal for building complex, maintainable systems.

## Core Principles of OOP

**Encapsulation** refers to bundling data and the methods that operate on that data within a single unit (a class), while restricting direct access to some components. This protects the internal state of objects and prevents unintended interference.

**Abstraction** means hiding complex implementation details and showing only the necessary features of an object. You interact with objects through well-defined interfaces without needing to understand their internal workings.

**Inheritance** allows you to create new classes based on existing ones, promoting code reuse. The derived class inherits properties and behaviors from the base class while being able to add or override functionality.

**Polymorphism** enables objects of different classes to be treated through the same interface. It allows a single function or operator to work in different ways depending on the context, either at compile-time or runtime.

## Classes and Objects

A class is a blueprint or template that defines the structure and behavior of objects. An object is an instance of a class, representing a concrete entity with actual values.

```cpp
class Car {
private:
    string brand;
    int speed;
    
public:
    // Constructor
    Car(string b, int s) : brand(b), speed(s) {}
    
    // Member functions
    void accelerate(int increment) {
        speed += increment;
    }
    
    void displayInfo() {
        cout << brand << " traveling at " << speed << " km/h" << endl;
    }
};

// Creating objects
Car myCar("Toyota", 60);
Car yourCar("Honda", 80);
```

## Access Specifiers

C++ provides three access specifiers that control visibility:

**Private** members are accessible only within the class itself. This is the default for class members and enforces encapsulation by hiding internal implementation.

**Protected** members are accessible within the class and by derived classes, allowing inheritance while maintaining encapsulation from external code.

**Public** members are accessible from anywhere in the program, forming the interface through which external code interacts with objects.

## Constructors and Destructors

**Constructors** are special member functions that initialize objects when they're created. They have the same name as the class and no return type.

```cpp
class Rectangle {
private:
    double width, height;
    
public:
    // Default constructor
    Rectangle() : width(0), height(0) {}
    
    // Parameterized constructor
    Rectangle(double w, double h) : width(w), height(h) {}
    
    // Copy constructor
    Rectangle(const Rectangle& other) : width(other.width), height(other.height) {}
};
```

**Destructors** clean up resources when an object is destroyed. They're called automatically and have the class name prefixed with a tilde (~).

```cpp
class FileHandler {
private:
    FILE* file;
    
public:
    FileHandler(const char* filename) {
        file = fopen(filename, "r");
    }
    
    ~FileHandler() {
        if (file) fclose(file);
    }
};
```

## Inheritance

Inheritance creates hierarchical relationships between classes, enabling code reuse and establishing "is-a" relationships.

```cpp
class Animal {
protected:
    string name;
    
public:
    Animal(string n) : name(n) {}
    
    void eat() {
        cout << name << " is eating" << endl;
    }
};

class Dog : public Animal {
private:
    string breed;
    
public:
    Dog(string n, string b) : Animal(n), breed(b) {}
    
    void bark() {
        cout << name << " says Woof!" << endl;
    }
};
```

**Types of Inheritance:**
- **Single inheritance**: One derived class inherits from one base class
- **Multiple inheritance**: One derived class inherits from multiple base classes
- **Multilevel inheritance**: A class inherits from a derived class
- **Hierarchical inheritance**: Multiple classes inherit from one base class
- **Hybrid inheritance**: Combination of multiple inheritance types

## Polymorphism

**Compile-time polymorphism** (static binding) is achieved through function overloading and operator overloading.

```cpp
class Calculator {
public:
    int add(int a, int b) { return a + b; }
    double add(double a, double b) { return a + b; }
    int add(int a, int b, int c) { return a + b + c; }
};
```

**Runtime polymorphism** (dynamic binding) uses virtual functions and is resolved during program execution.

```cpp
class Shape {
public:
    virtual double area() = 0;  // Pure virtual function
    virtual void draw() {
        cout << "Drawing a shape" << endl;
    }
};

class Circle : public Shape {
private:
    double radius;
    
public:
    Circle(double r) : radius(r) {}
    
    double area() override {
        return 3.14159 * radius * radius;
    }
    
    void draw() override {
        cout << "Drawing a circle" << endl;
    }
};

// Usage with polymorphism
Shape* shape = new Circle(5.0);
cout << "Area: " << shape->area() << endl;  // Calls Circle's area()
shape->draw();  // Calls Circle's draw()
```

## Abstract Classes and Interfaces

An **abstract class** contains at least one pure virtual function (declared with `= 0`) and cannot be instantiated. It serves as a base class for other classes to inherit from.

```cpp
class Database {
public:
    virtual void connect() = 0;
    virtual void query(string sql) = 0;
    virtual void disconnect() = 0;
};

class MySQLDatabase : public Database {
public:
    void connect() override {
        // MySQL-specific connection code
    }
    
    void query(string sql) override {
        // Execute MySQL query
    }
    
    void disconnect() override {
        // Close MySQL connection
    }
};
```

## Operator Overloading

C++ allows you to redefine the behavior of operators for user-defined types, making objects behave more intuitively.

```cpp
class Complex {
private:
    double real, imag;
    
public:
    Complex(double r = 0, double i = 0) : real(r), imag(i) {}
    
    Complex operator+(const Complex& other) {
        return Complex(real + other.real, imag + other.imag);
    }
    
    bool operator==(const Complex& other) {
        return real == other.real && imag == other.imag;
    }
    
    friend ostream& operator<<(ostream& os, const Complex& c) {
        os << c.real << " + " << c.imag << "i";
        return os;
    }
};
```

## Friend Functions and Classes

**Friend functions** can access private and protected members of a class despite not being member functions themselves.

```cpp
class Box {
private:
    double width;
    
public:
    Box(double w) : width(w) {}
    
    friend void printWidth(Box& box);
};

void printWidth(Box& box) {
    cout << "Width: " << box.width << endl;  // Can access private member
}
```

## Static Members

**Static data members** are shared by all objects of a class, existing independently of any instance.

**Static member functions** can only access static members and don't have access to the `this` pointer.

```cpp
class Counter {
private:
    static int count;
    int id;
    
public:
    Counter() {
        id = ++count;
    }
    
    static int getCount() {
        return count;
    }
};

int Counter::count = 0;  // Initialize static member
```

## The Four Pillars in Practice

When designing software with OOP in C++, you leverage encapsulation to protect data integrity, abstraction to simplify complex systems, inheritance to build upon existing code, and polymorphism to write flexible, extensible programs. Together, these principles enable you to create modular, maintainable, and scalable applications that model real-world problems effectively.