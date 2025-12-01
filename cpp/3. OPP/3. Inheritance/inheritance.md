# Inheritance in C++

## What is Inheritance?

**Inheritance** is a fundamental concept in Object-Oriented Programming (OOP) that allows a class to acquire properties (data members) and behaviors (member functions) from another class. It establishes an "IS-A" relationship between classes.

**Real-World Analogy:**
- A **Car** is a type of **Vehicle**
- A **Dog** is a type of **Animal**
- A **Student** is a type of **Person**

In these examples, Car, Dog, and Student inherit common characteristics from Vehicle, Animal, and Person respectively, while also having their own unique features.

## Key Terminology

- **Base Class (Parent/Super Class)**: The class whose properties are inherited
- **Derived Class (Child/Sub Class)**: The class that inherits from the base class
- **Inheritance**: The mechanism of deriving a new class from an existing class

## Why Use Inheritance?

1. **Code Reusability**: Reuse existing code without rewriting it
2. **Extensibility**: Add new features to existing classes
3. **Maintainability**: Changes in base class automatically reflect in derived classes
4. **Hierarchical Classification**: Organize classes in a logical hierarchy
5. **Polymorphism**: Foundation for runtime polymorphism

## Basic Syntax

```cpp
class BaseClass {
    // Base class members
};

class DerivedClass : access_specifier BaseClass {
    // Derived class members
};
```

## Types of Inheritance

### 1. Single Inheritance

One derived class inherits from one base class.

```
    Base
     |
  Derived
```

### 2. Multiple Inheritance

One derived class inherits from multiple base classes.

```
  Base1    Base2
     \      /
      Derived
```

### 3. Multilevel Inheritance

A derived class inherits from another derived class (chain of inheritance).

```
    Base
     |
  Derived1
     |
  Derived2
```

### 4. Hierarchical Inheritance

Multiple derived classes inherit from one base class.

```
      Base
    /  |  \
   D1  D2  D3
```

### 5. Hybrid Inheritance

Combination of two or more types of inheritance.

```
      Base
     /    \
   D1      D2
     \    /
       D3
```

## Access Specifiers in Inheritance

Access specifiers control how base class members are accessible in derived class:

| Base Class Member | Public Inheritance | Protected Inheritance | Private Inheritance |
|-------------------|-------------------|----------------------|---------------------|
| Public | Public | Protected | Private |
| Protected | Protected | Protected | Private |
| Private | Not Accessible | Not Accessible | Not Accessible |

**Key Points:**
- **Private members** of base class are NEVER directly accessible in derived class
- **Public inheritance**: IS-A relationship (most common)
- **Protected inheritance**: Rarely used
- **Private inheritance**: HAS-A relationship (composition alternative)

## Comprehensive ExamplesNow let me create a practical real-world example:## Important Inheritance Concepts

### 1. Constructor Execution Order

When creating a derived class object:
1. **Base class constructor** executes first
2. **Derived class constructor** executes second

When destroying a derived class object:
1. **Derived class destructor** executes first
2. **Base class destructor** executes second

```cpp
class Base {
public:
    Base() { cout << "Base constructor" << endl; }
    ~Base() { cout << "Base destructor" << endl; }
};

class Derived : public Base {
public:
    Derived() { cout << "Derived constructor" << endl; }
    ~Derived() { cout << "Derived destructor" << endl; }
};

// Creating object:
// Output: Base constructor
//         Derived constructor

// Destroying object:
// Output: Derived destructor
//         Base destructor
```

### 2. Function Overriding vs Function Overloading

**Function Overriding** (Inheritance):
- Same function name in base and derived class
- Same signature (parameters)
- Different implementation
- Uses `virtual` keyword for runtime polymorphism

**Function Overloading** (Same class):
- Same function name
- Different parameters
- Different signature

```cpp
class Base {
public:
    virtual void display() {
        cout << "Base display" << endl;
    }
};

class Derived : public Base {
public:
    void display() override {  // Overriding
        cout << "Derived display" << endl;
    }
    
    void display(int x) {  // Overloading
        cout << "Derived display: " << x << endl;
    }
};
```

### 3. The Diamond Problem

Occurs in **multiple inheritance** when a class inherits from two classes that have a common base class.

```
      Base
      /  \
     D1   D2
      \  /
      Final
```

**Problem**: Final has two copies of Base class members (ambiguity).

**Solution**: Use **virtual inheritance**

```cpp
class Base {
public:
    int value;
};

class D1 : virtual public Base {
    // ...
};

class D2 : virtual public Base {
    // ...
};

class Final : public D1, public D2 {
    // Now only one copy of Base exists
};
```

### 4. Virtual Functions and Polymorphism

**Virtual functions** enable **runtime polymorphism** (late binding).

```cpp
class Animal {
public:
    virtual void makeSound() {
        cout << "Animal sound" << endl;
    }
};

class Dog : public Animal {
public:
    void makeSound() override {
        cout << "Woof!" << endl;
    }
};

// Polymorphism in action
Animal* ptr = new Dog();
ptr->makeSound();  // Outputs: Woof! (not "Animal sound")
```

**Key Points:**
- Use `virtual` in base class
- Use `override` in derived class (C++11+)
- Enables dynamic dispatch
- Slight performance overhead
- Essential for polymorphism

### 5. Abstract Classes and Pure Virtual Functions

An **abstract class** contains at least one **pure virtual function** and cannot be instantiated.

```cpp
class Shape {  // Abstract class
public:
    virtual double area() = 0;  // Pure virtual function
    virtual void display() = 0;
};

class Circle : public Shape {
private:
    double radius;
public:
    Circle(double r) : radius(r) {}
    
    double area() override {
        return 3.14159 * radius * radius;
    }
    
    void display() override {
        cout << "Circle with area: " << area() << endl;
    }
};

// Shape s;  // ERROR: Cannot instantiate abstract class
Circle c(5.0);  // OK
```

## When to Use Inheritance

### ✅ Good Uses of Inheritance:

1. **True IS-A Relationship**: Dog IS-A Animal
2. **Code Reusability**: Common functionality in base class
3. **Polymorphic Behavior**: Different objects responding differently
4. **Extending Existing Classes**: Adding features without modifying original

### ❌ When NOT to Use Inheritance:

1. **HAS-A Relationship**: Use composition instead
   - Car HAS-A Engine (composition, not inheritance)
2. **Just for Code Reuse**: Consider composition or utility classes
3. **Tight Coupling**: If changes in base affect all derived classes badly
4. **Deep Hierarchies**: More than 3-4 levels becomes hard to maintain

## Inheritance vs Composition

**Inheritance**: "IS-A" relationship
```cpp
class Dog : public Animal {
    // Dog IS-A Animal
};
```

**Composition**: "HAS-A" relationship
```cpp
class Car {
private:
    Engine engine;  // Car HAS-A Engine
    Wheels wheels;  // Car HAS-A Wheels
};
```

**When to choose:**
- Use **inheritance** for specialization (Dog is a specialized Animal)
- Use **composition** for building complex objects from parts (Car has parts)

## Common Inheritance Mistakes

### 1. Not Making Destructor Virtual

```cpp
class Base {
public:
    ~Base() {  // Should be virtual!
        // cleanup
    }
};

class Derived : public Base {
private:
    int* data;
public:
    ~Derived() {
        delete[] data;  // May not be called!
    }
};

Base* ptr = new Derived();
delete ptr;  // Only Base destructor called - memory leak!
```

**Fix**: Always make base class destructor virtual

```cpp
class Base {
public:
    virtual ~Base() {
        // cleanup
    }
};
```

### 2. Slicing Problem

```cpp
class Base {
public:
    int x;
};

class Derived : public Base {
public:
    int y;
};

Derived d;
d.x = 10;
d.y = 20;

Base b = d;  // SLICING: y is lost!
cout << b.x;  // 10
// b.y doesn't exist
```

**Fix**: Use pointers or references

```cpp
Base* ptr = &d;  // No slicing
Base& ref = d;   // No slicing
```

### 3. Calling Virtual Functions in Constructor

```cpp
class Base {
public:
    Base() {
        initialize();  // Calls Base::initialize, not Derived!
    }
    virtual void initialize() {
        cout << "Base init" << endl;
    }
};

class Derived : public Base {
public:
    void initialize() override {
        cout << "Derived init" << endl;
    }
};

Derived d;  // Outputs: "Base init" (not "Derived init")
```

## Best Practices for Inheritance

1. **Keep inheritance hierarchies shallow** (2-3 levels max)
2. **Make base class destructors virtual**
3. **Use `override` keyword** for clarity (C++11+)
4. **Prefer composition over inheritance** when possible
5. **Follow Liskov Substitution Principle**: Derived class should be substitutable for base class
6. **Make member functions virtual only when needed**
7. **Use protected for members needed by derived classes**
8. **Document inheritance relationships clearly**
9. **Avoid multiple inheritance unless necessary**
10. **Use abstract classes to define interfaces**
