# Arithmetic Operators in C++

## Introduction
Arithmetic operators are used to perform mathematical operations on variables and constants. C++ provides a comprehensive set of arithmetic operators for basic and advanced mathematical computations.

## Basic Arithmetic Operators

### 1. Addition (`+`)
```cpp
#include <iostream>
using namespace std;

int main() {
    int a = 15, b = 7;
    int sum = a + b;
    
    cout << a << " + " << b << " = " << sum << endl;
    
    // Adding multiple numbers
    int total = a + b + 10 + 25;
    cout << "Total: " << total << endl;
    
    // Adding floating-point numbers
    double x = 5.5, y = 2.3;
    double result = x + y;
    cout << x << " + " << y << " = " << result << endl;
    
    return 0;
}
```

### 2. Subtraction (`-`)
```cpp
#include <iostream>
using namespace std;

int main() {
    int a = 20, b = 8;
    int difference = a - b;
    
    cout << a << " - " << b << " = " << difference << endl;
    
    // Negative results
    int negative = b - a;
    cout << b << " - " << a << " = " << negative << endl;
    
    // Floating-point subtraction
    double balance = 100.50;
    double withdrawal = 75.25;
    double remaining = balance - withdrawal;
    cout << "Balance: $" << balance << " - Withdrawal: $" << withdrawal 
         << " = Remaining: $" << remaining << endl;
    
    return 0;
}
```

### 3. Multiplication (`*`)
```cpp
#include <iostream>
using namespace std;

int main() {
    int length = 5, width = 3;
    int area = length * width;
    
    cout << "Area of rectangle: " << length << " * " << width 
         << " = " << area << endl;
    
    // Multiplication with different data types
    double price = 4.99;
    int quantity = 5;
    double total = price * quantity;  // int promoted to double
    
    cout << "Price: $" << price << " * Quantity: " << quantity 
         << " = Total: $" << total << endl;
    
    // Large numbers
    int big1 = 1000000, big2 = 2000000;
    long long bigProduct = (long long)big1 * big2;  // Cast to avoid overflow
    cout << big1 << " * " << big2 << " = " << bigProduct << endl;
    
    return 0;
}
```

### 4. Division (`/`)
```cpp
#include <iostream>
#include <iomanip>
using namespace std;

int main() {
    // Integer division
    int a = 10, b = 3;
    int intResult = a / b;
    cout << a << " / " << b << " = " << intResult 
         << " (integer division)" << endl;
    
    // Floating-point division
    double doubleResult = (double)a / b;
    cout << a << " / " << b << " = " << doubleResult 
         << " (floating-point division)" << endl;
    
    // Division with floating-point numbers
    double x = 10.0, y = 3.0;
    double divResult = x / y;
    cout << fixed << setprecision(3);
    cout << x << " / " << y << " = " << divResult << endl;
    
    // Division by zero
    int numerator = 5, zero = 0;
    // int error = numerator / zero;  // Runtime error - division by zero
    
    return 0;
}
```

### 5. Modulus (`%`)
```cpp
#include <iostream>
using namespace std;

int main() {
    // Basic modulus operations
    int a = 10, b = 3;
    int remainder = a % b;
    cout << a << " % " << b << " = " << remainder << endl;
    
    // Even/Odd check
    int number = 15;
    if (number % 2 == 0) {
        cout << number << " is even" << endl;
    } else {
        cout << number << " is odd" << endl;
    }
    
    // Divisibility check
    int year = 2024;
    if (year % 4 == 0) {
        cout << year << " is a leap year" << endl;
    } else {
        cout << year << " is not a leap year" << endl;
    }
    
    // Cycle through values
    for (int i = 0; i < 10; i++) {
        cout << i << " % 3 = " << (i % 3) << endl;
    }
    
    return 0;
}
```

## Increment and Decrement Operators

### Pre-increment vs Post-increment
```cpp
#include <iostream>
using namespace std;

int main() {
    int x = 5, y = 5;
    
    // Post-increment: use then increment
    cout << "Post-increment examples:" << endl;
    cout << "x = " << x << endl;
    cout << "x++ = " << x++ << endl;  // Prints 5, then x becomes 6
    cout << "x = " << x << endl;      // Now x is 6
    
    // Pre-increment: increment then use
    cout << "\nPre-increment examples:" << endl;
    cout << "y = " << y << endl;
    cout << "++y = " << ++y << endl;  // y becomes 6, then prints 6
    cout << "y = " << y << endl;      // y is 6
    
    // Practical example in loops
    cout << "\nLoop examples:" << endl;
    cout << "Post-increment in loop: ";
    for (int i = 0; i < 3; i++) {
        cout << i << " ";
    }
    
    cout << "\nPre-increment in loop: ";
    for (int i = 0; i < 3; ++i) {
        cout << i << " ";
    }
    cout << endl;
    
    return 0;
}
```

### Decrement Operators
```cpp
#include <iostream>
using namespace std;

int main() {
    int count = 5;
    
    // Post-decrement
    cout << "Post-decrement:" << endl;
    cout << "count = " << count << endl;
    cout << "count-- = " << count-- << endl;  // Prints 5, then becomes 4
    cout << "count = " << count << endl;
    
    // Pre-decrement
    cout << "\nPre-decrement:" << endl;
    cout << "count = " << count << endl;
    cout << "--count = " << --count << endl;  // Becomes 3, then prints 3
    cout << "count = " << count << endl;
    
    // Countdown example
    cout << "\nCountdown:" << endl;
    for (int i = 5; i > 0; --i) {
        cout << i << "... ";
    }
    cout << "Liftoff!" << endl;
    
    return 0;
}
```

## Compound Assignment Operators

```cpp
#include <iostream>
using namespace std;

int main() {
    int value = 10;
    
    // Addition assignment
    value += 5;  // Equivalent to: value = value + 5
    cout << "After += 5: " << value << endl;
    
    // Subtraction assignment
    value -= 3;  // Equivalent to: value = value - 3
    cout << "After -= 3: " << value << endl;
    
    // Multiplication assignment
    value *= 2;  // Equivalent to: value = value * 2
    cout << "After *= 2: " << value << endl;
    
    // Division assignment
    value /= 4;  // Equivalent to: value = value / 4
    cout << "After /= 4: " << value << endl;
    
    // Modulus assignment
    value %= 3;  // Equivalent to: value = value % 3
    cout << "After %= 3: " << value << endl;
    
    // Multiple operations
    int number = 100;
    number += 50;   // 150
    number -= 25;   // 125
    number *= 2;    // 250
    number /= 5;    // 50
    cout << "Final number: " << number << endl;
    
    return 0;
}
```

## Operator Precedence and Associativity

```cpp
#include <iostream>
using namespace std;

int main() {
    int a = 10, b = 5, c = 3, d = 2;
    
    // Demonstrating precedence
    int result1 = a + b * c;      // Multiplication first: 10 + (5 * 3) = 25
    int result2 = (a + b) * c;    // Parentheses first: (10 + 5) * 3 = 45
    int result3 = a * b / c;      // Left to right: (10 * 5) / 3 = 16
    int result4 = a + b % c;      // Modulus first: 10 + (5 % 3) = 12
    
    cout << "a + b * c = " << result1 << endl;
    cout << "(a + b) * c = " << result2 << endl;
    cout << "a * b / c = " << result3 << endl;
    cout << "a + b % c = " << result4 << endl;
    
    // Complex expression
    int complex = a + b * c - d / 2 + 10 % 3;
    // Step by step:
    // 1. b * c = 5 * 3 = 15
    // 2. d / 2 = 2 / 2 = 1
    // 3. 10 % 3 = 1
    // 4. a + 15 - 1 + 1 = 10 + 15 - 1 + 1 = 25
    
    cout << "Complex expression: " << complex << endl;
    
    return 0;
}
```

## Type Conversion in Arithmetic Operations

```cpp
#include <iostream>
using namespace std;

int main() {
    // Implicit type conversion
    int integer = 5;
    double decimal = 2.5;
    double result1 = integer + decimal;  // int promoted to double
    cout << integer << " + " << decimal << " = " << result1 << endl;
    
    // Explicit type casting
    int a = 10, b = 3;
    double result2 = (double)a / b;      // Explicit cast
    cout << a << " / " << b << " = " << result2 << endl;
    
    // Mixed-type expressions
    int x = 7;
    float y = 2.5f;
    double z = 1.5;
    
    auto result3 = x + y + z;  // All promoted to double
    cout << "Type of result3: " << typeid(result3).name() << endl;
    cout << "Value: " << result3 << endl;
    
    // Character arithmetic
    char letter = 'A';
    cout << "Letter: " << letter << endl;
    cout << "Letter + 1: " << (char)(letter + 1) << endl;  // 'B'
    cout << "ASCII value: " << (int)letter << endl;        // 65
    
    return 0;
}
```

## Practical Examples

### Calculator Program
```cpp
#include <iostream>
using namespace std;

int main() {
    double num1, num2;
    char operation;
    
    cout << "Simple Calculator" << endl;
    cout << "Enter first number: ";
    cin >> num1;
    
    cout << "Enter operation (+, -, *, /): ";
    cin >> operation;
    
    cout << "Enter second number: ";
    cin >> num2;
    
    double result;
    bool validOperation = true;
    
    switch (operation) {
        case '+':
            result = num1 + num2;
            break;
        case '-':
            result = num1 - num2;
            break;
        case '*':
            result = num1 * num2;
            break;
        case '/':
            if (num2 != 0) {
                result = num1 / num2;
            } else {
                cout << "Error: Division by zero!" << endl;
                validOperation = false;
            }
            break;
        default:
            cout << "Error: Invalid operation!" << endl;
            validOperation = false;
    }
    
    if (validOperation) {
        cout << num1 << " " << operation << " " << num2 << " = " << result << endl;
    }
    
    return 0;
}
```

### Temperature Converter
```cpp
#include <iostream>
#include <iomanip>
using namespace std;

int main() {
    double celsius, fahrenheit;
    
    cout << "Temperature Converter" << endl;
    cout << "Enter temperature in Celsius: ";
    cin >> celsius;
    
    // Convert to Fahrenheit
    fahrenheit = (celsius * 9.0 / 5.0) + 32.0;
    
    cout << fixed << setprecision(2);
    cout << celsius << "°C = " << fahrenheit << "°F" << endl;
    
    return 0;
}
```

### Compound Interest Calculator
```cpp
#include <iostream>
#include <cmath>    // For pow() function
#include <iomanip>
using namespace std;

int main() {
    double principal, rate, time, compoundInterest;
    int compoundFrequency;
    
    cout << "Compound Interest Calculator" << endl;
    cout << "Enter principal amount: $";
    cin >> principal;
    
    cout << "Enter annual interest rate (%): ";
    cin >> rate;
    
    cout << "Enter time in years: ";
    cin >> time;
    
    cout << "Enter compound frequency (times per year): ";
    cin >> compoundFrequency;
    
    // Convert percentage to decimal
    rate = rate / 100.0;
    
    // Calculate compound interest: A = P(1 + r/n)^(nt)
    double amount = principal * pow(1 + rate / compoundFrequency, compoundFrequency * time);
    compoundInterest = amount - principal;
    
    cout << fixed << setprecision(2);
    cout << "\nResults:" << endl;
    cout << "Principal: $" << principal << endl;
    cout << "Compound Interest: $" << compoundInterest << endl;
    cout << "Total Amount: $" << amount << endl;
    
    return 0;
}
```

## Common Pitfalls and Best Practices

```cpp
#include <iostream>
#include <limits>
using namespace std;

int main() {
    // 1. Integer division when expecting floating-point
    int a = 7, b = 2;
    double wrong = a / b;           // Wrong: 3.0 (integer division)
    double correct = (double)a / b; // Correct: 3.5
    
    cout << "Wrong: " << wrong << endl;
    cout << "Correct: " << correct << endl;
    
    // 2. Integer overflow
    int maxInt = numeric_limits<int>::max();
    cout << "Max int: " << maxInt << endl;
    // int overflow = maxInt + 1;  // Undefined behavior
    
    // 3. Division by zero
    int numerator = 5, zero = 0;
    // int error = numerator / zero;  // Runtime error
    
    // 4. Precision loss
    double bigNumber = 1.0e20;
    double smallNumber = 1.0;
    double sum = bigNumber + smallNumber;
    cout << "Precision loss: " << bigNumber << " + " << smallNumber 
         << " = " << sum << " (may lose precision)" << endl;
    
    return 0;
}
```