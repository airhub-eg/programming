# Loops in C++

## Introduction to Loops
Loops are control structures that allow repeated execution of a block of code. They are essential for automating repetitive tasks, processing collections of data, and implementing iterative algorithms.

## 1. The `for` Loop

### Basic `for` Loop
```cpp
#include <iostream>
using namespace std;

int main() {
    // Basic for loop: print numbers 1 to 5
    for (int i = 1; i <= 5; i++) {
        cout << i << " ";
    }
    cout << endl;
    
    // Counting backwards
    for (int i = 5; i >= 1; i--) {
        cout << i << " ";
    }
    cout << endl;
    
    // With different increment
    for (int i = 0; i <= 10; i += 2) {
        cout << i << " ";
    }
    cout << endl;
    
    return 0;
}
```

### Advanced `for` Loop Patterns
```cpp
#include <iostream>
using namespace std;

int main() {
    // Sum of first N numbers
    int n, sum = 0;
    cout << "Enter a number: ";
    cin >> n;
    
    for (int i = 1; i <= n; i++) {
        sum += i;
    }
    cout << "Sum of first " << n << " numbers: " << sum << endl;
    
    // Factorial calculation
    long long factorial = 1;
    for (int i = 1; i <= n; i++) {
        factorial *= i;
    }
    cout << n << "! = " << factorial << endl;
    
    // Multiplication table
    int number;
    cout << "Enter number for multiplication table: ";
    cin >> number;
    
    for (int i = 1; i <= 10; i++) {
        cout << number << " × " << i << " = " << (number * i) << endl;
    }
    
    return 0;
}
```

### Multiple Variables in `for` Loop
```cpp
#include <iostream>
using namespace std;

int main() {
    // Multiple initialization and update
    for (int i = 0, j = 10; i < j; i++, j--) {
        cout << "i = " << i << ", j = " << j << endl;
    }
    
    // Fibonacci sequence using for loop
    int terms;
    cout << "Enter number of terms for Fibonacci: ";
    cin >> terms;
    
    long long a = 0, b = 1;
    cout << "Fibonacci sequence: ";
    
    for (int i = 0; i < terms; i++) {
        cout << a << " ";
        long long next = a + b;
        a = b;
        b = next;
    }
    cout << endl;
    
    return 0;
}
```

## 2. The `while` Loop

### Basic `while` Loop
```cpp
#include <iostream>
using namespace std;

int main() {
    // Basic while loop
    int count = 1;
    while (count <= 5) {
        cout << "Count: " << count << endl;
        count++;
    }
    
    // User input validation with while
    int number;
    cout << "Enter a positive number: ";
    cin >> number;
    
    while (number <= 0) {
        cout << "Invalid input! Enter a positive number: ";
        cin >> number;
    }
    cout << "Thank you! You entered: " << number << endl;
    
    return 0;
}
```

### `while` Loop with Complex Conditions
```cpp
#include <iostream>
using namespace std;

int main() {
    // Password validation
    string correctPassword = "secret123";
    string userPassword;
    int attempts = 0;
    const int MAX_ATTEMPTS = 3;
    
    cout << "Enter password: ";
    cin >> userPassword;
    
    while (userPassword != correctPassword && attempts < MAX_ATTEMPTS - 1) {
        attempts++;
        cout << "Incorrect password! Attempts remaining: " 
             << (MAX_ATTEMPTS - attempts) << endl;
        cout << "Enter password: ";
        cin >> userPassword;
    }
    
    if (userPassword == correctPassword) {
        cout << "Access granted!" << endl;
    } else {
        cout << "Access denied! Too many failed attempts." << endl;
    }
    
    return 0;
}
```

### Sentinel-Controlled `while` Loop
```cpp
#include <iostream>
using namespace std;

int main() {
    // Sentinel-controlled loop (terminates with specific value)
    int score;
    int sum = 0;
    int count = 0;
    
    cout << "Enter test scores (-1 to stop): ";
    cin >> score;
    
    while (score != -1) {
        sum += score;
        count++;
        cout << "Enter next score (-1 to stop): ";
        cin >> score;
    }
    
    if (count > 0) {
        double average = static_cast<double>(sum) / count;
        cout << "Average score: " << average << endl;
    } else {
        cout << "No scores entered." << endl;
    }
    
    return 0;
}
```

## 3. The `do-while` Loop

### Basic `do-while` Loop
```cpp
#include <iostream>
using namespace std;

int main() {
    // do-while loop (executes at least once)
    int number;
    
    do {
        cout << "Enter a number between 1 and 10: ";
        cin >> number;
    } while (number < 1 || number > 10);
    
    cout << "Thank you! You entered: " << number << endl;
    
    return 0;
}
```

### Menu System with `do-while`
```cpp
#include <iostream>
using namespace std;

int main() {
    int choice;
    
    do {
        // Display menu
        cout << "\n=== Calculator Menu ===" << endl;
        cout << "1. Add two numbers" << endl;
        cout << "2. Subtract two numbers" << endl;
        cout << "3. Multiply two numbers" << endl;
        cout << "4. Divide two numbers" << endl;
        cout << "5. Exit" << endl;
        cout << "Enter your choice (1-5): ";
        cin >> choice;
        
        if (choice >= 1 && choice <= 4) {
            double num1, num2, result;
            cout << "Enter first number: ";
            cin >> num1;
            cout << "Enter second number: ";
            cin >> num2;
            
            switch (choice) {
                case 1:
                    result = num1 + num2;
                    cout << "Result: " << result << endl;
                    break;
                case 2:
                    result = num1 - num2;
                    cout << "Result: " << result << endl;
                    break;
                case 3:
                    result = num1 * num2;
                    cout << "Result: " << result << endl;
                    break;
                case 4:
                    if (num2 != 0) {
                        result = num1 / num2;
                        cout << "Result: " << result << endl;
                    } else {
                        cout << "Error: Division by zero!" << endl;
                    }
                    break;
            }
        } else if (choice != 5) {
            cout << "Invalid choice! Please try again." << endl;
        }
        
    } while (choice != 5);
    
    cout << "Thank you for using the calculator!" << endl;
    
    return 0;
}
```

## 4. Range-based `for` Loop (C++11)

### Basic Range-based Loop
```cpp
#include <iostream>
#include <vector>
#include <array>
#include <string>
using namespace std;

int main() {
    // Range-based for loop with array
    int numbers[] = {1, 2, 3, 4, 5};
    
    cout << "Array elements: ";
    for (int num : numbers) {
        cout << num << " ";
    }
    cout << endl;
    
    // With vector
    vector<string> fruits = {"apple", "banana", "orange", "grape"};
    
    cout << "Fruits: ";
    for (const string& fruit : fruits) {
        cout << fruit << " ";
    }
    cout << endl;
    
    // Modifying elements with reference
    vector<int> values = {1, 2, 3, 4, 5};
    cout << "Original values: ";
    for (int val : values) {
        cout << val << " ";
    }
    cout << endl;
    
    // Double each value using reference
    for (int& val : values) {
        val *= 2;
    }
    
    cout << "Doubled values: ";
    for (int val : values) {
        cout << val << " ";
    }
    cout << endl;
    
    return 0;
}
```

### Range-based Loop with `auto`
```cpp
#include <iostream>
#include <vector>
#include <map>
using namespace std;

int main() {
    // Using auto with range-based for loop
    vector<double> temperatures = {25.5, 30.2, 18.7, 22.4, 27.8};
    
    cout << "Temperatures: ";
    for (auto temp : temperatures) {
        cout << temp << "°C ";
    }
    cout << endl;
    
    // With map
    map<string, int> ageMap = {
        {"Alice", 25},
        {"Bob", 30},
        {"Charlie", 35},
        {"Diana", 28}
    };
    
    cout << "Ages:" << endl;
    for (const auto& entry : ageMap) {
        cout << entry.first << ": " << entry.second << " years" << endl;
    }
    
    // Structured bindings (C++17)
    #if __cplusplus >= 201703L
    cout << "\nUsing structured bindings:" << endl;
    for (const auto& [name, age] : ageMap) {
        cout << name << ": " << age << " years" << endl;
    }
    #endif
    
    return 0;
}
```

## 5. Loop Control Statements

### `break` Statement
```cpp
#include <iostream>
using namespace std;

int main() {
    // break in for loop
    cout << "Searching for number 5: ";
    for (int i = 1; i <= 10; i++) {
        if (i == 5) {
            cout << "Found it! ";
            break;  // Exit loop immediately
        }
        cout << i << " ";
    }
    cout << endl;
    
    // break in while loop
    int number;
    while (true) {  // Infinite loop
        cout << "Enter a number (0 to stop): ";
        cin >> number;
        
        if (number == 0) {
            break;  // Exit infinite loop
        }
        
        cout << "You entered: " << number << endl;
    }
    
    cout << "Program ended." << endl;
    
    return 0;
}
```

### `continue` Statement
```cpp
#include <iostream>
using namespace std;

int main() {
    // continue example: print odd numbers
    cout << "Odd numbers from 1 to 10: ";
    for (int i = 1; i <= 10; i++) {
        if (i % 2 == 0) {
            continue;  // Skip even numbers
        }
        cout << i << " ";
    }
    cout << endl;
    
    // Skip negative numbers in sum
    int number, sum = 0;
    cout << "Enter numbers (0 to stop):" << endl;
    
    while (true) {
        cin >> number;
        
        if (number == 0) {
            break;
        }
        
        if (number < 0) {
            cout << "Skipping negative number: " << number << endl;
            continue;  // Skip negative numbers
        }
        
        sum += number;
    }
    
    cout << "Sum of positive numbers: " << sum << endl;
    
    return 0;
}
```

## 6. Nested Loops

### Basic Nested Loops
```cpp
#include <iostream>
using namespace std;

int main() {
    // Multiplication table using nested loops
    cout << "Multiplication Table (1-5):" << endl;
    cout << "    ";
    
    // Print header
    for (int i = 1; i <= 5; i++) {
        cout << i << "   ";
    }
    cout << endl;
    
    // Print table
    for (int i = 1; i <= 5; i++) {
        cout << i << " | ";
        for (int j = 1; j <= 5; j++) {
            cout << (i * j) << "  ";
        }
        cout << endl;
    }
    
    return 0;
}
```

### Pattern Printing with Nested Loops
```cpp
#include <iostream>
using namespace std;

int main() {
    int rows;
    
    cout << "Enter number of rows: ";
    cin >> rows;
    
    // Right triangle pattern
    cout << "\nRight Triangle Pattern:" << endl;
    for (int i = 1; i <= rows; i++) {
        for (int j = 1; j <= i; j++) {
            cout << "* ";
        }
        cout << endl;
    }
    
    // Pyramid pattern
    cout << "\nPyramid Pattern:" << endl;
    for (int i = 1; i <= rows; i++) {
        // Print spaces
        for (int j = 1; j <= rows - i; j++) {
            cout << "  ";
        }
        // Print stars
        for (int j = 1; j <= (2 * i - 1); j++) {
            cout << "* ";
        }
        cout << endl;
    }
    
    // Number pyramid
    cout << "\nNumber Pyramid:" << endl;
    for (int i = 1; i <= rows; i++) {
        for (int j = 1; j <= rows - i; j++) {
            cout << "  ";
        }
        for (int j = 1; j <= i; j++) {
            cout << j << " ";
        }
        for (int j = i - 1; j >= 1; j--) {
            cout << j << " ";
        }
        cout << endl;
    }
    
    return 0;
}
```

## 7. Practical Loop Applications

### Array Processing
```cpp
#include <iostream>
using namespace std;

int main() {
    const int SIZE = 5;
    int arr[SIZE];
    
    // Input array elements
    cout << "Enter " << SIZE << " integers:" << endl;
    for (int i = 0; i < SIZE; i++) {
        cout << "Element " << (i + 1) << ": ";
        cin >> arr[i];
    }
    
    // Find maximum and minimum
    int max = arr[0];
    int min = arr[0];
    int sum = 0;
    
    for (int i = 0; i < SIZE; i++) {
        if (arr[i] > max) {
            max = arr[i];
        }
        if (arr[i] < min) {
            min = arr[i];
        }
        sum += arr[i];
    }
    
    double average = static_cast<double>(sum) / SIZE;
    
    cout << "\nArray Analysis:" << endl;
    cout << "Maximum: " << max << endl;
    cout << "Minimum: " << min << endl;
    cout << "Sum: " << sum << endl;
    cout << "Average: " << average << endl;
    
    // Search for an element
    int searchValue;
    cout << "\nEnter a value to search: ";
    cin >> searchValue;
    
    bool found = false;
    int position = -1;
    
    for (int i = 0; i < SIZE; i++) {
        if (arr[i] == searchValue) {
            found = true;
            position = i;
            break;
        }
    }
    
    if (found) {
        cout << "Value " << searchValue << " found at position " << position << endl;
    } else {
        cout << "Value " << searchValue << " not found in array." << endl;
    }
    
    return 0;
}
```

### Prime Number Checker
```cpp
#include <iostream>
#include <cmath>
using namespace std;

int main() {
    int number;
    
    cout << "Enter a number to check if it's prime: ";
    cin >> number;
    
    if (number <= 1) {
        cout << number << " is not prime." << endl;
        return 0;
    }
    
    bool isPrime = true;
    
    // Check divisibility from 2 to sqrt(number)
    for (int i = 2; i <= sqrt(number); i++) {
        if (number % i == 0) {
            isPrime = false;
            break;
        }
    }
    
    if (isPrime) {
        cout << number << " is prime." << endl;
    } else {
        cout << number << " is not prime." << endl;
    }
    
    // Generate prime numbers in a range
    int start, end;
    cout << "\nEnter range to find primes (start end): ";
    cin >> start >> end;
    
    cout << "Prime numbers between " << start << " and " << end << ":" << endl;
    
    for (int num = start; num <= end; num++) {
        if (num <= 1) continue;
        
        bool isCurrentPrime = true;
        for (int i = 2; i <= sqrt(num); i++) {
            if (num % i == 0) {
                isCurrentPrime = false;
                break;
            }
        }
        
        if (isCurrentPrime) {
            cout << num << " ";
        }
    }
    cout << endl;
    
    return 0;
}
```

## 8. Infinite Loops and Their Uses

### Intentional Infinite Loops
```cpp
#include <iostream>
using namespace std;

int main() {
    // Server-like application using infinite loop
    int requestCount = 0;
    
    cout << "Server started. Press Ctrl+C to stop." << endl;
    
    while (true) {
        requestCount++;
        cout << "Processing request #" << requestCount << endl;
        
        // Simulate some work
        for (int i = 0; i < 100000000; i++) {
            // Busy wait
        }
        
        // Break condition (in real applications, use signals)
        if (requestCount >= 5) {
            cout << "Simulated server shutdown after 5 requests." << endl;
            break;
        }
    }
    
    // Game loop example
    char input;
    int score = 0;
    
    cout << "\nSimple Game - Press 'q' to quit, any other key to score:" << endl;
    
    while (true) {
        cout << "Enter input: ";
        cin >> input;
        
        if (input == 'q' || input == 'Q') {
            break;
        }
        
        score++;
        cout << "Score: " << score << endl;
    }
    
    cout << "Game over! Final score: " << score << endl;
    
    return 0;
}
```

## 9. Loop Optimization Techniques

### Efficient Loop Patterns
```cpp
#include <iostream>
#include <vector>
#include <chrono>
using namespace std;
using namespace std::chrono;

int main() {
    const int SIZE = 1000000;
    vector<int> data(SIZE, 1);
    
    // Method 1: Traditional loop
    auto start1 = high_resolution_clock::now();
    
    int sum1 = 0;
    for (int i = 0; i < SIZE; i++) {
        sum1 += data[i];
    }
    
    auto stop1 = high_resolution_clock::now();
    auto duration1 = duration_cast<microseconds>(stop1 - start1);
    
    // Method 2: Precompute loop bound
    auto start2 = high_resolution_clock::now();
    
    int sum2 = 0;
    int bound = SIZE;
    for (int i = 0; i < bound; i++) {
        sum2 += data[i];
    }
    
    auto stop2 = high_resolution_clock::now();
    auto duration2 = duration_cast<microseconds>(stop2 - start2);
    
    // Method 3: Range-based loop
    auto start3 = high_resolution_clock::now();
    
    int sum3 = 0;
    for (int value : data) {
        sum3 += value;
    }
    
    auto stop3 = high_resolution_clock::now();
    auto duration3 = duration_cast<microseconds>(stop3 - start3);
    
    cout << "Sum results: " << sum1 << ", " << sum2 << ", " << sum3 << endl;
    cout << "Execution times:" << endl;
    cout << "Traditional: " << duration1.count() << " microseconds" << endl;
    cout << "Precomputed: " << duration2.count() << " microseconds" << endl;
    cout << "Range-based: " << duration3.count() << " microseconds" << endl;
    
    return 0;
}
```

## 10. Complete Practical Example: Student Management System

```cpp
#include <iostream>
#include <vector>
#include <string>
#include <iomanip>
using namespace std;

struct Student {
    string name;
    int id;
    double grade;
};

int main() {
    vector<Student> students;
    int choice;
    
    do {
        cout << "\n=== Student Management System ===" << endl;
        cout << "1. Add Student" << endl;
        cout << "2. Display All Students" << endl;
        cout << "3. Calculate Average Grade" << endl;
        cout << "4. Find Highest Grade" << endl;
        cout << "5. Search Student by ID" << endl;
        cout << "6. Exit" << endl;
        cout << "Enter your choice: ";
        cin >> choice;
        
        switch (choice) {
            case 1: {
                Student newStudent;
                cout << "Enter student name: ";
                cin.ignore();
                getline(cin, newStudent.name);
                cout << "Enter student ID: ";
                cin >> newStudent.id;
                cout << "Enter student grade: ";
                cin >> newStudent.grade;
                
                students.push_back(newStudent);
                cout << "Student added successfully!" << endl;
                break;
            }
            
            case 2: {
                if (students.empty()) {
                    cout << "No students to display." << endl;
                } else {
                    cout << "\n" << setw(5) << "ID" << setw(20) << "Name" 
                         << setw(10) << "Grade" << endl;
                    cout << string(35, '-') << endl;
                    
                    for (const Student& student : students) {
                        cout << setw(5) << student.id << setw(20) << student.name 
                             << setw(10) << student.grade << endl;
                    }
                }
                break;
            }
            
            case 3: {
                if (students.empty()) {
                    cout << "No students to calculate average." << endl;
                } else {
                    double total = 0;
                    for (const Student& student : students) {
                        total += student.grade;
                    }
                    double average = total / students.size();
                    cout << "Average grade: " << fixed << setprecision(2) << average << endl;
                }
                break;
            }
            
            case 4: {
                if (students.empty()) {
                    cout << "No students to find highest grade." << endl;
                } else {
                    double highest = students[0].grade;
                    string topStudent = students[0].name;
                    
                    for (const Student& student : students) {
                        if (student.grade > highest) {
                            highest = student.grade;
                            topStudent = student.name;
                        }
                    }
                    cout << "Highest grade: " << highest << " by " << topStudent << endl;
                }
                break;
            }
            
            case 5: {
                if (students.empty()) {
                    cout << "No students to search." << endl;
                } else {
                    int searchId;
                    cout << "Enter student ID to search: ";
                    cin >> searchId;
                    
                    bool found = false;
                    for (const Student& student : students) {
                        if (student.id == searchId) {
                            cout << "Student found:" << endl;
                            cout << "Name: " << student.name << endl;
                            cout << "ID: " << student.id << endl;
                            cout << "Grade: " << student.grade << endl;
                            found = true;
                            break;
                        }
                    }
                    
                    if (!found) {
                        cout << "Student with ID " << searchId << " not found." << endl;
                    }
                }
                break;
            }
            
            case 6:
                cout << "Exiting program. Goodbye!" << endl;
                break;
                
            default:
                cout << "Invalid choice! Please try again." << endl;
        }
        
    } while (choice != 6);
    
    return 0;
}
```
