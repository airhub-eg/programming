# Basic Input/Output (I/O) in C++

## Introduction to I/O Streams
C++ uses streams for input and output operations. The main streams are:
- `cin` for input (console in)
- `cout` for output (console out)
- `cerr` for error output
- `clog` for logging

## Basic Header and Setup
```cpp
#include <iostream>  // Required for basic I/O
using namespace std; // Allows using cout, cin without std::

// Alternative: use std:: prefix
// std::cout, std::cin, std::endl
```

## Output with `cout`

### Basic Output
```cpp
#include <iostream>
using namespace std;

int main() {
    // Simple output
    cout << "Hello, World!" << endl;
    
    // Output multiple items
    cout << "The answer is " << 42 << endl;
    
    // Mathematical expressions
    cout << "5 + 3 = " << (5 + 3) << endl;
    
    return 0;
}
```

### Formatting Output
```cpp
#include <iostream>
#include <iomanip>  // For output formatting
using namespace std;

int main() {
    int number = 123;
    double price = 19.9876;
    
    // Setting decimal precision
    cout << fixed << setprecision(2);
    cout << "Price: $" << price << endl;
    
    // Setting width for output
    cout << "Number: " << setw(10) << number << endl;
    
    // Fill characters
    cout << "Filled: " << setw(10) << setfill('*') << number << endl;
    
    // Boolean formatting
    bool isTrue = true;
    cout << boolalpha;  // Display true/false instead of 1/0
    cout << "Boolean value: " << isTrue << endl;
    
    // Scientific notation
    double bigNumber = 123456789.0;
    cout << scientific << "Scientific: " << bigNumber << endl;
    
    return 0;
}
```

## Input with `cin`

### Basic Input
```cpp
#include <iostream>
using namespace std;

int main() {
    int age;
    string name;
    double salary;
    
    // Single input
    cout << "Enter your age: ";
    cin >> age;
    
    // Multiple inputs
    cout << "Enter your name and salary: ";
    cin >> name >> salary;
    
    cout << "Hello " << name << ", age " << age 
         << ", salary: $" << salary << endl;
    
    return 0;
}
```

### Handling Different Data Types
```cpp
#include <iostream>
using namespace std;

int main() {
    // Integer input
    int number;
    cout << "Enter an integer: ";
    cin >> number;
    
    // Floating-point input
    double decimal;
    cout << "Enter a decimal number: ";
    cin >> decimal;
    
    // Character input
    char initial;
    cout << "Enter your initial: ";
    cin >> initial;
    
    // Boolean input (1/0 or true/false)
    bool isEmployed;
    cout << "Are you employed? (1 for yes, 0 for no): ";
    cin >> isEmployed;
    
    cout << "\n--- Summary ---" << endl;
    cout << "Integer: " << number << endl;
    cout << "Decimal: " << decimal << endl;
    cout << "Initial: " << initial << endl;
    cout << "Employed: " << boolalpha << isEmployed << endl;
    
    return 0;
}
```

## String Input

### Using `cin` for Strings
```cpp
#include <iostream>
#include <string>  // Required for string type
using namespace std;

int main() {
    string firstName, fullName;
    
    // cin for single word
    cout << "Enter your first name: ";
    cin >> firstName;
    
    // Clear the input buffer
    cin.ignore();
    
    // getline for full line with spaces
    cout << "Enter your full name: ";
    getline(cin, fullName);
    
    cout << "First name: " << firstName << endl;
    cout << "Full name: " << fullName << endl;
    
    return 0;
}
```

### Handling Multiple Lines
```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string line1, line2;
    
    cout << "Enter first line: ";
    getline(cin, line1);
    
    cout << "Enter second line: ";
    getline(cin, line2);
    
    cout << "\nYou entered:" << endl;
    cout << "Line 1: " << line1 << endl;
    cout << "Line 2: " << line2 << endl;
    
    return 0;
}
```

## Error Handling in Input

### Checking Input Validity
```cpp
#include <iostream>
using namespace std;

int main() {
    int number;
    
    cout << "Enter a number: ";
    
    // Check if input is valid
    if (cin >> number) {
        cout << "Valid input: " << number << endl;
    } else {
        cout << "Invalid input!" << endl;
        // Clear error state
        cin.clear();
        // Ignore invalid input
        cin.ignore(1000, '\n');
    }
    
    return 0;
}
```

### Robust Input with Validation
```cpp
#include <iostream>
using namespace std;

int main() {
    int age;
    
    while (true) {
        cout << "Enter your age (1-120): ";
        
        if (cin >> age) {
            if (age >= 1 && age <= 120) {
                break;  // Valid input, exit loop
            } else {
                cout << "Age must be between 1 and 120!" << endl;
            }
        } else {
            cout << "Please enter a valid number!" << endl;
            cin.clear();
            cin.ignore(1000, '\n');
        }
    }
    
    cout << "Thank you! Your age is: " << age << endl;
    
    return 0;
}
```

## File I/O Basics

### Reading from Files
```cpp
#include <iostream>
#include <fstream>  // File stream
#include <string>
using namespace std;

int main() {
    ifstream inputFile;  // Input file stream
    string filename, line;
    
    cout << "Enter filename to read: ";
    cin >> filename;
    
    inputFile.open(filename);
    
    if (inputFile.is_open()) {
        cout << "File contents:" << endl;
        while (getline(inputFile, line)) {
            cout << line << endl;
        }
        inputFile.close();
    } else {
        cout << "Unable to open file: " << filename << endl;
    }
    
    return 0;
}
```

### Writing to Files
```cpp
#include <iostream>
#include <fstream>
using namespace std;

int main() {
    ofstream outputFile;  // Output file stream
    string filename, content;
    
    cout << "Enter filename to write: ";
    cin >> filename;
    
    outputFile.open(filename);
    
    if (outputFile.is_open()) {
        cout << "Enter content (type 'END' on separate line to finish):" << endl;
        cin.ignore();  // Clear buffer
        
        while (true) {
            getline(cin, content);
            if (content == "END") break;
            outputFile << content << endl;
        }
        
        outputFile.close();
        cout << "Content written to " << filename << endl;
    } else {
        cout << "Unable to create file!" << endl;
    }
    
    return 0;
}
```

## Complete Practical Example: Student Registration

```cpp
#include <iostream>
#include <iomanip>
#include <string>
using namespace std;

int main() {
    string name, course;
    int age;
    double gpa;
    
    // Display header
    cout << "=== STUDENT REGISTRATION SYSTEM ===" << endl;
    cout << setfill('=') << setw(40) << "" << setfill(' ') << endl;
    
    // Get student information
    cout << "Enter student name: ";
    getline(cin, name);
    
    cout << "Enter age: ";
    cin >> age;
    
    cout << "Enter course: ";
    cin.ignore();  // Clear buffer
    getline(cin, course);
    
    cout << "Enter GPA: ";
    cin >> gpa;
    
    // Display formatted output
    cout << "\n" << setfill('=') << setw(40) << "" << setfill(' ') << endl;
    cout << "REGISTRATION COMPLETE" << endl;
    cout << setfill('-') << setw(40) << "" << setfill(' ') << endl;
    
    cout << left << setw(15) << "Name:" << name << endl;
    cout << left << setw(15) << "Age:" << age << endl;
    cout << left << setw(15) << "Course:" << course << endl;
    cout << fixed << setprecision(2);
    cout << left << setw(15) << "GPA:" << gpa << endl;
    
    // Conditional message based on GPA
    if (gpa >= 3.5) {
        cout << "\nExcellent! You qualify for honors." << endl;
    } else if (gpa >= 2.0) {
        cout << "\nGood standing." << endl;
    } else {
        cout << "\nAcademic warning." << endl;
    }
    
    return 0;
}
```

## Error Streams: `cerr` and `clog`

```cpp
#include <iostream>
using namespace std;

int main() {
    int number;
    
    cout << "Enter a positive number: ";
    cin >> number;
    
    if (number <= 0) {
        // Use cerr for error messages (unbuffered)
        cerr << "ERROR: Number must be positive!" << endl;
        
        // Use clog for log messages (buffered)
        clog << "Invalid input detected: " << number << endl;
    } else {
        cout << "Valid number: " << number << endl;
    }
    
    return 0;
}
```
