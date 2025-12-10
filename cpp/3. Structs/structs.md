# Structs in C++

## 1. **Introduction to Structs**

A **struct** (short for structure) in C++ is a user-defined data type that groups together variables of different types under a single name. Structs are fundamental building blocks for creating complex data types.

```cpp
// Basic struct definition
struct Point {
    int x;
    int y;
};
```

## 2. **Key Characteristics**

### Default Access Specifiers
- **Struct**: Members are `public` by default
- **Class**: Members are `private` by default (this is the only technical difference)

```cpp
struct MyStruct {  // members are public by default
    int data;
};

class MyClass {    // members are private by default
    int data;
};
```

## 3. **Struct Declaration and Definition**

### Basic Syntax
```cpp
struct StructName {
    // member variables
    type1 member1;
    type2 member2;
    
    // member functions (methods)
    returnType methodName(parameters);
};
```

### Example with Various Data Types
```cpp
struct Employee {
    // Data members
    int id;
    std::string name;
    double salary;
    std::string department;
    
    // Member function
    void display() {
        std::cout << "ID: " << id << "\nName: " << name 
                  << "\nSalary: $" << salary << std::endl;
    }
};
```

## 4. **Creating and Using Struct Instances**

### Declaration and Initialization
```cpp
// Method 1: Direct initialization
Point p1 = {10, 20};

// Method 2: Using designated initializers (C++20)
Point p2 = {.x = 5, .y = 15};

// Method 3: Create then assign
Point p3;
p3.x = 30;
p3.y = 40;

// Method 4: Uniform initialization (C++11)
Point p4{25, 35};
```

### Accessing Members
```cpp
Employee emp;
emp.id = 1001;
emp.name = "John Doe";
emp.salary = 75000.50;
emp.display();
```

## 5. **Advanced Struct Features**

### Constructors and Destructors
```cpp
struct Rectangle {
    double length;
    double width;
    
    // Default constructor
    Rectangle() : length(0), width(0) {}
    
    // Parameterized constructor
    Rectangle(double l, double w) : length(l), width(w) {}
    
    // Copy constructor
    Rectangle(const Rectangle& other) 
        : length(other.length), width(other.width) {}
    
    // Destructor
    ~Rectangle() {
        // Cleanup code if needed
    }
    
    // Member function
    double area() const {
        return length * width;
    }
};
```

### Operator Overloading
```cpp
struct Vector2D {
    double x, y;
    
    Vector2D operator+(const Vector2D& other) const {
        return {x + other.x, y + other.y};
    }
    
    Vector2D operator*(double scalar) const {
        return {x * scalar, y * scalar};
    }
    
    bool operator==(const Vector2D& other) const {
        return x == other.x && y == other.y;
    }
};
```

## 6. **Structs with Dynamic Memory**

```cpp
struct Student {
    std::string name;
    int* grades;  // Dynamic array
    int numGrades;
    
    // Constructor
    Student(const std::string& n, int num) 
        : name(n), numGrades(num) {
        grades = new int[num];
    }
    
    // Destructor to prevent memory leak
    ~Student() {
        delete[] grades;
    }
    
    // Copy constructor (deep copy)
    Student(const Student& other) 
        : name(other.name), numGrades(other.numGrades) {
        grades = new int[numGrades];
        std::copy(other.grades, other.grades + numGrades, grades);
    }
    
    // Copy assignment operator
    Student& operator=(const Student& other) {
        if (this != &other) {
            delete[] grades;
            name = other.name;
            numGrades = other.numGrades;
            grades = new int[numGrades];
            std::copy(other.grades, other.grades + numGrades, grades);
        }
        return *this;
    }
};
```

## 7. **Nested and Anonymous Structs**

### Nested Structs
```cpp
struct Address {
    std::string street;
    std::string city;
    std::string zipCode;
};

struct Person {
    std::string name;
    int age;
    Address homeAddress;  // Nested struct
    Address workAddress;
};
```

### Anonymous Structs
```cpp
struct {
    int x, y;
} point;  // Anonymous struct with variable 'point'

// Usage
point.x = 10;
point.y = 20;
```

## 8. **Structs with Static Members**

```cpp
struct Counter {
    static int totalCount;  // Static member variable
    
    int id;
    
    Counter() {
        id = ++totalCount;
    }
    
    static void reset() {  // Static member function
        totalCount = 0;
    }
};

// Initialize static member
int Counter::totalCount = 0;
```

## 9. **Bit Fields in Structs**

Useful for memory optimization when dealing with hardware or protocols:

```cpp
struct Register {
    unsigned int flag1 : 1;   // 1 bit
    unsigned int flag2 : 1;   // 1 bit
    unsigned int mode  : 3;   // 3 bits
    unsigned int value : 11;  // 11 bits
    // Total: 16 bits (2 bytes)
};
```

## 10. **Aggregate Initialization**

Structs support aggregate initialization if:
- All members are public
- No user-declared constructors
- No base classes
- No virtual functions

```cpp
struct AggregateExample {
    int a;
    double b;
    char c[10];
};

AggregateExample ex = {42, 3.14, "Hello"};
```

## 11. **Structs vs Classes: When to Use Which**

### Use **struct** when:
- You have a simple data container
- All members should be public by default
- You're implementing a POD (Plain Old Data) type
- You need C compatibility

### Use **class** when:
- You need encapsulation
- Members should be private by default
- You're implementing complex behavior
- You need strict access control

## 12. **Modern C++ Features with Structs**

### Structured Bindings (C++17)
```cpp
struct Coordinate {
    double latitude;
    double longitude;
    double altitude;
};

Coordinate getPosition() {
    return {40.7128, -74.0060, 10.5};
}

auto [lat, lon, alt] = getPosition();  // Decompose struct
```

### Designated Initializers (C++20)
```cpp
struct Config {
    int timeout = 30;
    std::string host = "localhost";
    int port = 8080;
};

Config config {
    .timeout = 60,
    .host = "example.com",
    .port = 443
};
```

## 13. **Best Practices**

1. **Use structs for passive data** with public members
2. **Initialize all members** to avoid undefined behavior
3. **Follow the Rule of Five/Zero** when managing resources
4. **Make member functions `const`** when they don't modify the object
5. **Consider move semantics** for large structs
6. **Use `[[nodiscard]]`** for factory functions
7. **Document your structs** with comments

```cpp
// Well-designed struct example
struct [[nodiscard]] Measurement {
    double value;
    std::string unit;
    time_t timestamp;
    
    // Const member function
    std::string toString() const {
        return std::to_string(value) + " " + unit;
    }
    
    // Factory function
    static Measurement create(double val, const std::string& u) {
        return {val, u, std::time(nullptr)};
    }
};
```

## 14. **Complete Example**

```cpp
#include <iostream>
#include <string>
#include <vector>

struct Book {
    // Data members
    std::string title;
    std::string author;
    int publicationYear;
    double price;
    
    // Constructor with member initializer list
    Book(const std::string& t, const std::string& a, int year, double p)
        : title(t), author(a), publicationYear(year), price(p) {}
    
    // Const member function
    void display() const {
        std::cout << "Title: " << title 
                  << "\nAuthor: " << author
                  << "\nYear: " << publicationYear
                  << "\nPrice: $" << price << "\n\n";
    }
    
    // Operator overload for sorting
    bool operator<(const Book& other) const {
        return title < other.title;
    }
};

int main() {
    // Create a collection of books
    std::vector<Book> library = {
        {"The C++ Programming Language", "Bjarne Stroustrup", 2013, 79.99},
        {"Effective Modern C++", "Scott Meyers", 2014, 49.99},
        {"Clean Code", "Robert C. Martin", 2008, 39.99}
    };
    
    // Display all books
    for (const auto& book : library) {
        book.display();
    }
    
    return 0;
}
```

## 15. **Performance Considerations**

1. **Memory Layout**: Structs have contiguous memory layout
2. **Padding and Alignment**: Compiler may insert padding for alignment
3. **Cache Friendly**: Sequential access patterns are efficient
4. **Pass by Value/Reference**: Small structs can be passed by value, large ones by reference

```cpp
// Use references for large structs
void processLargeStruct(const BigStruct& data) {
    // Efficient - no copying
}

// Pass small structs by value
void processPoint(Point p) {
    // Efficient for small types
}
```