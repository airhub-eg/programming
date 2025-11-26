# Namespaces in C++

## What is a Namespace?

A **namespace** is a declarative region that provides a scope to the identifiers (names of types, functions, variables, etc.) inside it. Namespaces are used to organize code into logical groups and to prevent name collisions that can occur especially when your code base includes multiple libraries.

Think of namespaces as containers that hold a set of identifiers. They help avoid naming conflicts when different parts of a program use the same identifier names.

## Why Use Namespaces?

### Problem Without Namespaces

Imagine you're working on a project that uses two different libraries, and both define a function called `print()`:

```cpp
// Library A
void print() {
    cout << "Library A print" << endl;
}

// Library B
void print() {
    cout << "Library B print" << endl;
}

// Your code
int main() {
    print();  // ERROR: Which print() should be called?
}
```

This creates a naming conflict. Namespaces solve this problem.

### Solution With Namespaces

```cpp
// Library A
namespace LibraryA {
    void print() {
        cout << "Library A print" << endl;
    }
}

// Library B
namespace LibraryB {
    void print() {
        cout << "Library B print" << endl;
    }
}

// Your code
int main() {
    LibraryA::print();  // Clearly calls Library A's print
    LibraryB::print();  // Clearly calls Library B's print
}
```

## Defining Namespaces

### Basic Syntax

```cpp
namespace namespace_name {
    // declarations and definitions
    // variables, functions, classes, etc.
}
```

### Simple Example

```cpp
#include <iostream>
using namespace std;

namespace MyNamespace {
    int value = 100;
    
    void display() {
        cout << "Value: " << value << endl;
    }
    
    class MyClass {
    public:
        void greet() {
            cout << "Hello from MyClass" << endl;
        }
    };
}

int main() {
    cout << MyNamespace::value << endl;
    MyNamespace::display();
    
    MyNamespace::MyClass obj;
    obj.greet();
    
    return 0;
}
```

## Accessing Namespace Members

There are several ways to access members of a namespace:

### 1. Scope Resolution Operator (::)

The most explicit and recommended way:

```cpp
namespace Math {
    const double PI = 3.14159;
    
    double square(double x) {
        return x * x;
    }
}

int main() {
    cout << Math::PI << endl;
    cout << Math::square(5) << endl;
}
```

### 2. Using Declaration

Brings a specific member into the current scope:

```cpp
namespace Math {
    double square(double x) { return x * x; }
    double cube(double x) { return x * x * x; }
}

int main() {
    using Math::square;  // Only 'square' is now accessible without Math::
    
    cout << square(5) << endl;     // OK
    cout << Math::cube(5) << endl; // Must still use Math::
    // cout << cube(5);            // ERROR
}
```

### 3. Using Directive

Brings all members of a namespace into the current scope:

```cpp
namespace Math {
    double square(double x) { return x * x; }
    double cube(double x) { return x * x * x; }
}

int main() {
    using namespace Math;  // All Math members accessible
    
    cout << square(5) << endl;  // OK
    cout << cube(5) << endl;    // OK
}
```

**Warning**: Using directives in header files or global scope is generally discouraged as it defeats the purpose of namespaces.

## The std Namespace

The C++ Standard Library uses the `std` namespace for all its components:

```cpp
#include <iostream>
#include <vector>
#include <string>

int main() {
    std::cout << "Hello World" << std::endl;
    std::vector<int> numbers = {1, 2, 3, 4, 5};
    std::string text = "C++ Programming";
    
    for (const auto& num : numbers) {
        std::cout << num << " ";
    }
}
```

### Common Debate: `using namespace std;`

```cpp
// Approach 1: Explicit (Recommended for large projects)
#include <iostream>

int main() {
    std::cout << "Hello" << std::endl;
}

// Approach 2: Using directive (OK for small programs)
#include <iostream>
using namespace std;

int main() {
    cout << "Hello" << endl;
}

// Approach 3: Selective using (Good compromise)
#include <iostream>
using std::cout;
using std::endl;

int main() {
    cout << "Hello" << endl;
    std::vector<int> v;  // Still need std:: for vector
}
```

**Best Practice**: 
- Avoid `using namespace std;` in header files
- Avoid it in global scope of large projects
- OK to use in small programs or function scope
- Prefer selective `using` declarations when needed

## Nested Namespaces

Namespaces can be nested inside other namespaces:

### Traditional Syntax

```cpp
namespace Outer {
    int value1 = 10;
    
    namespace Inner {
        int value2 = 20;
        
        void display() {
            cout << "Inner value: " << value2 << endl;
            cout << "Outer value: " << value1 << endl;  // Can access outer
        }
    }
}

int main() {
    cout << Outer::value1 << endl;
    cout << Outer::Inner::value2 << endl;
    Outer::Inner::display();
}
```

### Compact Syntax (C++17)

```cpp
// Instead of:
namespace A {
    namespace B {
        namespace C {
            void func() { }
        }
    }
}

// You can write:
namespace A::B::C {
    void func() { }
}

// Access:
int main() {
    A::B::C::func();
}
```

### Real-World Example

```cpp
namespace Company {
    namespace ProjectX {
        namespace Utils {
            void log(const string& msg) {
                cout << "[ProjectX Utils] " << msg << endl;
            }
        }
        
        namespace Core {
            void process() {
                Utils::log("Processing data...");
            }
        }
    }
}

// C++17 alternative:
namespace Company::ProjectX::Utils {
    void log(const string& msg) {
        cout << "[ProjectX Utils] " << msg << endl;
    }
}
```

## Unnamed (Anonymous) Namespaces

An unnamed namespace provides internal linkage, similar to the `static` keyword. Members are unique to the translation unit (source file) and cannot be accessed from other files.

```cpp
// file1.cpp
namespace {
    int internalValue = 100;  // Only visible in file1.cpp
    
    void helperFunction() {
        cout << "Helper in file1" << endl;
    }
}

void publicFunction() {
    helperFunction();  // OK
    cout << internalValue << endl;  // OK
}

// file2.cpp
void anotherFunction() {
    // helperFunction();  // ERROR: Not visible here
    // cout << internalValue;  // ERROR: Not visible here
}
```

### When to Use Unnamed Namespaces

```cpp
// header.h
void publicAPI();

// implementation.cpp
namespace {
    // Internal implementation details
    constexpr int BUFFER_SIZE = 1024;
    
    bool validateInput(const string& input) {
        return !input.empty();
    }
    
    class InternalHelper {
        // Implementation details
    };
}

void publicAPI() {
    // Use internal helpers
    if (validateInput("data")) {
        InternalHelper helper;
        // ...
    }
}
```

**Benefits**:
- Prevents naming conflicts between translation units
- Clearly marks internal implementation details
- Compiler can optimize better (internal linkage)

## Namespace Aliases

Create shorter names for long namespace names:

```cpp
namespace VeryLongCompanyNamespaceForProject {
    void someFunction() {
        cout << "Function called" << endl;
    }
}

int main() {
    // Create alias
    namespace VLCNFP = VeryLongCompanyNamespaceForProject;
    
    VLCNFP::someFunction();  // Much easier to type!
}
```

### Practical Example

```cpp
namespace filesystem = std::filesystem;  // C++17

int main() {
    filesystem::path p = "/home/user/file.txt";
    // Instead of: std::filesystem::path p = ...
}
```

### Nested Namespace Aliases

```cpp
namespace Company::Project::Module::SubModule {
    void func() { }
}

int main() {
    namespace SM = Company::Project::Module::SubModule;
    SM::func();
}
```

## Extending Namespaces

You can add to a namespace in multiple places, even across different files:

### Same File

```cpp
namespace MyNamespace {
    void func1() {
        cout << "Function 1" << endl;
    }
}

// Later in the same file
namespace MyNamespace {
    void func2() {
        cout << "Function 2" << endl;
    }
}

int main() {
    MyNamespace::func1();
    MyNamespace::func2();  // Both are in MyNamespace
}
```

### Multiple Files

```cpp
// math.h
namespace Math {
    double add(double a, double b);
}

// math.cpp
namespace Math {
    double add(double a, double b) {
        return a + b;
    }
}

// advanced_math.h
namespace Math {  // Extending Math namespace
    double power(double base, double exp);
}

// advanced_math.cpp
namespace Math {
    double power(double base, double exp) {
        return pow(base, exp);
    }
}
```

## Inline Namespaces (C++11)

Inline namespaces are automatically accessible from their enclosing namespace. They're primarily used for versioning:

```cpp
namespace MyLib {
    inline namespace v2 {  // Current version
        void process() {
            cout << "Processing v2" << endl;
        }
    }
    
    namespace v1 {  // Old version
        void process() {
            cout << "Processing v1" << endl;
        }
    }
}

int main() {
    MyLib::process();     // Calls v2 (inline)
    MyLib::v2::process(); // Explicitly v2
    MyLib::v1::process(); // Explicitly v1
}
```

### Versioning Example

```cpp
namespace MyLibrary {
    inline namespace Version_2_0 {
        class Widget {
        public:
            void render() {
                cout << "Rendering with new algorithm" << endl;
            }
        };
    }
    
    namespace Version_1_0 {
        class Widget {
        public:
            void render() {
                cout << "Rendering with old algorithm" << endl;
            }
        };
    }
}

int main() {
    MyLibrary::Widget w;  // Uses Version_2_0 automatically
    w.render();
    
    MyLibrary::Version_1_0::Widget oldW;  // Legacy code can use old version
    oldW.render();
}
```

## Namespace Usage in Headers and Source Files

### Best Practices

**header.h**:
```cpp
#ifndef HEADER_H
#define HEADER_H

#include <string>

// NEVER do this in a header:
// using namespace std;  // BAD!

namespace MyProject {
    class MyClass {
    private:
        std::string name;  // Always use std:: in headers
        
    public:
        MyClass(const std::string& n);
        void display() const;
        std::string getName() const;
    };
    
    void helperFunction(const std::string& msg);
}

#endif
```

**source.cpp**:
```cpp
#include "header.h"
#include <iostream>

// OK to use 'using' in source files
using std::cout;
using std::endl;

namespace MyProject {
    MyClass::MyClass(const std::string& n) : name(n) { }
    
    void MyClass::display() const {
        cout << "Name: " << name << endl;
    }
    
    std::string MyClass::getName() const {
        return name;
    }
    
    void helperFunction(const std::string& msg) {
        cout << "Helper: " << msg << endl;
    }
}
```

**main.cpp**:
```cpp
#include "header.h"
#include <iostream>

int main() {
    // Option 1: Fully qualified
    MyProject::MyClass obj1("Object1");
    obj1.display();
    
    // Option 2: Using declaration
    using MyProject::MyClass;
    MyClass obj2("Object2");
    obj2.display();
    
    // Option 3: Using directive (local scope)
    {
        using namespace MyProject;
        MyClass obj3("Object3");
        helperFunction("Test");
    }
    
    return 0;
}
```

## Name Lookup and Argument-Dependent Lookup (ADL)

ADL, also called Koenig lookup, allows functions to be found based on the types of their arguments:

```cpp
namespace MyNamespace {
    class MyClass { };
    
    void func(MyClass obj) {
        cout << "MyNamespace::func called" << endl;
    }
}

int main() {
    MyNamespace::MyClass obj;
    
    // Both of these work due to ADL:
    MyNamespace::func(obj);  // Explicit
    func(obj);               // ADL finds it automatically
}
```

### Why ADL Matters

```cpp
namespace std {
    // This is how operator<< works for cout
    // ostream& operator<<(ostream&, const string&);
}

int main() {
    std::string s = "Hello";
    
    // This works because of ADL:
    std::cout << s;  // operator<< found via ADL
    
    // Without ADL, you'd need:
    // std::operator<<(std::cout, s);
}
```

### ADL Example with Custom Types

```cpp
namespace Math {
    struct Point {
        double x, y;
    };
    
    // Found via ADL when using Point
    void print(const Point& p) {
        cout << "(" << p.x << ", " << p.y << ")" << endl;
    }
    
    Point operator+(const Point& a, const Point& b) {
        return {a.x + b.x, a.y + b.y};
    }
}

int main() {
    Math::Point p1{1.0, 2.0};
    Math::Point p2{3.0, 4.0};
    
    print(p1);  // ADL finds Math::print
    
    Math::Point p3 = p1 + p2;  // ADL finds Math::operator+
    print(p3);
}
```

## Global Namespace

The global namespace is the default namespace without any name:

```cpp
// Global namespace
int globalVar = 100;

void globalFunction() {
    cout << "Global function" << endl;
}

namespace MyNamespace {
    int globalVar = 200;  // Different from ::globalVar
    
    void test() {
        cout << globalVar << endl;    // 200 (MyNamespace::globalVar)
        cout << ::globalVar << endl;  // 100 (global namespace)
        
        globalFunction();    // Calls global function
        ::globalFunction();  // Explicitly calls global function
    }
}
```

### Accessing Global Namespace Explicitly

```cpp
int value = 42;

namespace MyNamespace {
    int value = 99;
    
    void display() {
        cout << "Local value: " << value << endl;     // 99
        cout << "Global value: " << ::value << endl;  // 42
    }
}
```

## Practical Examples

### Example 1: Organizing a Game Project

```cpp
// game.h
namespace Game {
    namespace Graphics {
        class Renderer {
        public:
            void render();
        };
        
        class Sprite {
        public:
            void draw();
        };
    }
    
    namespace Audio {
        class SoundManager {
        public:
            void playSound(const std::string& name);
        };
    }
    
    namespace Physics {
        class Engine {
        public:
            void update(float deltaTime);
        };
    }
}

// Usage
int main() {
    Game::Graphics::Renderer renderer;
    Game::Audio::SoundManager audio;
    Game::Physics::Engine physics;
    
    // Or with aliases
    namespace GFX = Game::Graphics;
    namespace SND = Game::Audio;
    
    GFX::Sprite sprite;
    SND::SoundManager soundMgr;
}
```

### Example 2: Mathematical Utilities

```cpp
#include <iostream>
#include <cmath>
using namespace std;

namespace MathUtils {
    namespace Geometry {
        const double PI = 3.14159265359;
        
        double circleArea(double radius) {
            return PI * radius * radius;
        }
        
        double circleCircumference(double radius) {
            return 2 * PI * radius;
        }
        
        namespace ThreeD {
            double sphereVolume(double radius) {
                return (4.0 / 3.0) * PI * radius * radius * radius;
            }
        }
    }
    
    namespace Statistics {
        double mean(const vector<double>& data) {
            double sum = 0;
            for (double val : data) sum += val;
            return sum / data.size();
        }
        
        double variance(const vector<double>& data) {
            double m = mean(data);
            double sum = 0;
            for (double val : data) {
                sum += (val - m) * (val - m);
            }
            return sum / data.size();
        }
    }
}

int main() {
    // Using full qualification
    cout << "Circle area: " 
         << MathUtils::Geometry::circleArea(5.0) << endl;
    
    // Using alias
    namespace Geo = MathUtils::Geometry;
    cout << "Sphere volume: " 
         << Geo::ThreeD::sphereVolume(3.0) << endl;
    
    // Using declaration
    using MathUtils::Statistics::mean;
    vector<double> data = {1.0, 2.0, 3.0, 4.0, 5.0};
    cout << "Mean: " << mean(data) << endl;
    
    return 0;
}
```

### Example 3: Configuration System

```cpp
namespace Config {
    namespace Database {
        inline namespace Production {
            const string HOST = "prod-db.example.com";
            const int PORT = 5432;
            const string NAME = "production_db";
        }
        
        namespace Development {
            const string HOST = "localhost";
            const int PORT = 5432;
            const string NAME = "dev_db";
        }
    }
    
    namespace API {
        inline namespace V2 {
            const string BASE_URL = "https://api.example.com/v2";
            const int TIMEOUT = 30;
        }
        
        namespace V1 {
            const string BASE_URL = "https://api.example.com/v1";
            const int TIMEOUT = 60;
        }
    }
}

int main() {
    // Uses Production and V2 by default (inline)
    cout << "DB Host: " << Config::Database::HOST << endl;
    cout << "API URL: " << Config::API::BASE_URL << endl;
    
    // Can explicitly use other versions
    cout << "Dev DB: " << Config::Database::Development::HOST << endl;
    cout << "Old API: " << Config::API::V1::BASE_URL << endl;
}
```

### Example 4: Library with Internal Implementation

```cpp
// mylib.h
#ifndef MYLIB_H
#define MYLIB_H

#include <string>
#include <vector>

namespace MyLib {
    class DataProcessor {
    public:
        DataProcessor();
        void process(const std::vector<int>& data);
        std::string getResult() const;
        
    private:
        std::string result;
    };
}

#endif

// mylib.cpp
#include "mylib.h"
#include <sstream>
#include <algorithm>

namespace {  // Anonymous namespace for internal helpers
    bool isEven(int n) {
        return n % 2 == 0;
    }
    
    int square(int n) {
        return n * n;
    }
    
    std::string formatOutput(const std::vector<int>& numbers) {
        std::ostringstream oss;
        oss << "[";
        for (size_t i = 0; i < numbers.size(); ++i) {
            oss << numbers[i];
            if (i < numbers.size() - 1) oss << ", ";
        }
        oss << "]";
        return oss.str();
    }
}

namespace MyLib {
    DataProcessor::DataProcessor() : result("") { }
    
    void DataProcessor::process(const std::vector<int>& data) {
        std::vector<int> processed;
        
        for (int num : data) {
            if (isEven(num)) {  // Uses anonymous namespace function
                processed.push_back(square(num));
            }
        }
        
        result = formatOutput(processed);
    }
    
    std::string DataProcessor::getResult() const {
        return result;
    }
}

// main.cpp
#include "mylib.h"
#include <iostream>
using namespace std;

int main() {
    MyLib::DataProcessor processor;
    vector<int> data = {1, 2, 3, 4, 5, 6, 7, 8};
    
    processor.process(data);
    cout << processor.getResult() << endl;  // [4, 16, 36, 64]
    
    return 0;
}
```

## Common Pitfalls and Best Practices

### Pitfall 1: Using Namespace in Headers

```cpp
// BAD - header.h
#include <string>
using namespace std;  // DON'T DO THIS!

class MyClass {
    string name;  // Now anyone including this header gets 'using namespace std'
};

// GOOD - header.h
#include <string>

class MyClass {
    std::string name;  // Always use std:: in headers
};
```

### Pitfall 2: Name Collisions

```cpp
namespace A {
    void func() { cout << "A::func" << endl; }
}

namespace B {
    void func() { cout << "B::func" << endl; }
}

int main() {
    using namespace A;
    using namespace B;
    
    func();  // ERROR: Ambiguous! Which func()?
    
    // Solution: Be explicit
    A::func();
    B::func();
}
```

### Pitfall 3: Forgetting Namespace in Implementation

```cpp
// header.h
namespace MyNamespace {
    class MyClass {
    public:
        void method();
    };
}

// source.cpp - WRONG
void MyClass::method() {  // ERROR: MyClass not in global scope
    // ...
}

// source.cpp - CORRECT
namespace MyNamespace {
    void MyClass::method() {
        // ...
    }
}

// OR
void MyNamespace::MyClass::method() {
    // ...
}
```

### Best Practice 1: Namespace Naming

```cpp
// Good naming conventions
namespace company_name { }
namespace project_name { }
namespace module_name { }

// Use lowercase with underscores
namespace my_library { }

// For nested, use clear hierarchy
namespace MyCompany::ProjectX::Database { }
```

### Best Practice 2: Limit Using Directives

```cpp
// OK in function scope
void myFunction() {
    using namespace std;
    cout << "Local scope is fine" << endl;
}

// AVOID in global scope
// using namespace std;  // Affects entire file

// BETTER: Selective using
using std::cout;
using std::endl;
using std::vector;
```

### Best Practice 3: Organize Large Projects

```cpp
// Project structure
namespace CompanyName {
    namespace ProjectName {
        namespace Core {
            // Core functionality
        }
        
        namespace Utils {
            // Utility functions
        }
        
        namespace Internal {
            // Internal implementation details
            namespace {
                // File-local helpers
            }
        }
    }
}
```

## Summary

Namespaces are a fundamental feature of C++ that help organize code and prevent naming conflicts. Key points to remember:

1. **Purpose**: Organize code and avoid name collisions
2. **Access**: Use `::` scope resolution operator
3. **std Namespace**: Contains all standard library components
4. **Using Directives**: Convenient but use carefully
5. **Anonymous Namespaces**: For internal linkage (file-local)
6. **Nested Namespaces**: Organize hierarchically
7. **Inline Namespaces**: For versioning
8. **Best Practices**: 
   - Don't use `using` in headers
   - Be explicit in headers with `std::`
   - Use namespaces to organize large projects
   - Prefer selective `using` declarations over directives

Namespaces are your friends in creating maintainable, collision-free C++ code!