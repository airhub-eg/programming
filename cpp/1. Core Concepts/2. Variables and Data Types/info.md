# Variables and Data Types in C++

## What are Variables?
Variables are named storage locations in memory that hold data which can be changed during program execution. They act as containers for storing information.

## Basic Variable Syntax
```cpp
data_type variable_name = value;
```

## Fundamental Data Types in C++

### 1. Integer Types
Store whole numbers without decimal points.

```cpp
#include <iostream>
using namespace std;

int main() {
    // Different integer types
    short smallNumber = 100;          // Typically 2 bytes (-32,768 to 32,767)
    int age = 25;                    // Typically 4 bytes (-2.1B to 2.1B)
    long bigNumber = 123456789L;     // Typically 4 or 8 bytes
    long long veryBigNumber = 123456789012345LL; // Typically 8 bytes
    
    // Unsigned integers (only positive)
    unsigned int positiveNumber = 40000;
    unsigned short smallPositive = 65000;
    
    cout << "Age: " << age << endl;
    cout << "Big Number: " << bigNumber << endl;
    
    return 0;
}
```

### 2. Floating-Point Types
Store numbers with decimal points.

```cpp
#include <iostream>
#include <iomanip>  // For setprecision
using namespace std;

int main() {
    float price = 19.99f;           // Single precision, ~7 decimal digits
    double distance = 12345.6789;   // Double precision, ~15 decimal digits
    long double preciseValue = 3.141592653589793238L; // Extended precision
    
    cout << fixed << setprecision(2);
    cout << "Price: $" << price << endl;
    cout << "Distance: " << distance << " meters" << endl;
    cout << "Pi: " << preciseValue << endl;
    
    // Scientific notation
    double scientific = 1.5e-5;  // 0.000015
    cout << "Scientific: " << scientific << endl;
    
    return 0;
}
```

### 3. Character Types
Store single characters.

```cpp
#include <iostream>
using namespace std;

int main() {
    char grade = 'A';           // Single character
    char newline = '\n';        // Escape sequence
    char tab = '\t';
    
    // Wide characters for international characters
    wchar_t wideChar = L'Ω';
    
    cout << "Grade: " << grade << endl;
    cout << "Name" << tab << "Age" << endl;
    
    // Characters are stored as ASCII values
    char letter = 65;  // ASCII value for 'A'
    cout << "Letter from ASCII: " << letter << endl;
    
    return 0;
}
```

### 4. Boolean Type
Represents true or false values.

```cpp
#include <iostream>
using namespace std;

int main() {
    bool isSunny = true;
    bool isRaining = false;
    bool hasPassed = (75 >= 50);  // Expression evaluates to true
    
    cout << boolalpha;  // Display true/false instead of 1/0
    cout << "Is it sunny? " << isSunny << endl;
    cout << "Is it raining? " << isRaining << endl;
    cout << "Has student passed? " << hasPassed << endl;
    
    // Boolean in conditions
    if (isSunny && !isRaining) {
        cout << "Perfect weather for a walk!" << endl;
    }
    
    return 0;
}
```

### 5. Void Type
Represents the absence of type.

```cpp
#include <iostream>
using namespace std;

// Function that doesn't return a value
void printMessage() {
    cout << "Hello from void function!" << endl;
    // No return statement needed
}

int main() {
    printMessage();
    return 0;
}
```

## Type Modifiers

### Signed and Unsigned
```cpp
#include <iostream>
using namespace std;

int main() {
    signed int negativeNumber = -100;    // Can be positive or negative
    unsigned int positiveOnly = 30000;   // Only positive numbers
    
    signed char sc = -128;               // Range: -128 to 127
    unsigned char uc = 255;              // Range: 0 to 255
    
    cout << "Negative: " << negativeNumber << endl;
    cout << "Positive Only: " << positiveOnly << endl;
    
    return 0;
}
```

## Variable Declaration and Initialization

```cpp
#include <iostream>
using namespace std;

int main() {
    // Different ways to initialize variables
    int a;           // Declaration (uninitialized - contains garbage value)
    int b = 10;      // Initialization with assignment
    int c(20);       // Direct initialization
    int d{30};       // Uniform initialization (C++11)
    int e = {40};    // Copy list initialization
    
    // Multiple variable declaration
    int x = 1, y = 2, z = 3;
    
    // Constants
    const double PI = 3.14159;
    const int MAX_SIZE = 100;
    
    cout << "b = " << b << ", c = " << c << ", d = " << d << endl;
    cout << "PI = " << PI << endl;
    
    // PI = 3.14;  // Error: cannot modify constant
    
    return 0;
}
```

## Auto Keyword (C++11)
Let the compiler deduce the type automatically.

```cpp
#include <iostream>
#include <typeinfo>  // For typeid
using namespace std;

int main() {
    auto number = 42;           // int
    auto price = 19.99;         // double
    auto name = "John";         // const char*
    auto isActive = true;       // bool
    
    cout << "number type: " << typeid(number).name() << endl;
    cout << "price type: " << typeid(price).name() << endl;
    cout << "name type: " << typeid(name).name() << endl;
    
    // Useful with complex types
    auto result = number * price;
    cout << "Result: " << result << endl;
    
    return 0;
}
```

## Type Conversion

```cpp
#include <iostream>
using namespace std;

int main() {
    // Implicit conversion
    int integer = 10;
    double decimal = integer;  // int to double
    cout << "Integer to double: " << decimal << endl;
    
    double pi = 3.14159;
    int approx = pi;           // double to int (truncation)
    cout << "Double to int: " << approx << endl;
    
    // Explicit conversion (C-style cast)
    int x = 10, y = 3;
    double division = (double)x / y;
    cout << "Division: " << division << endl;
    
    // C++ style casts
    double value = 9.87;
    int intValue = static_cast<int>(value);
    cout << "Static cast: " << intValue << endl;
    
    return 0;
}
```

