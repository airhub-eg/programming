# Functions in C++

## Introduction to Functions
Functions are self-contained blocks of code that perform specific tasks. They promote code reusability, modularity, and make programs easier to understand and maintain.

## 1. Function Declaration and Definition

### Basic Function Structure
```cpp
#include <iostream>
using namespace std;

// Function declaration (prototype)
int add(int a, int b);

// Function definition
int add(int a, int b) {
    return a + b;
}

// Function without parameters and return value
void greet() {
    cout << "Hello, World!" << endl;
}

int main() {
    // Function calls
    greet();
    
    int result = add(5, 3);
    cout << "5 + 3 = " << result << endl;
    
    return 0;
}
```

### Separate Declaration and Definition
```cpp
#include <iostream>
using namespace std;

// Function declarations (in header file typically)
double calculateCircleArea(double radius);
void printMessage(string message, int times);
int getMax(int a, int b, int c);

int main() {
    double area = calculateCircleArea(5.0);
    cout << "Circle area: " << area << endl;
    
    printMessage("C++ is fun!", 3);
    
    int maxVal = getMax(10, 25, 15);
    cout << "Maximum value: " << maxVal << endl;
    
    return 0;
}

// Function definitions
double calculateCircleArea(double radius) {
    const double PI = 3.14159;
    return PI * radius * radius;
}

void printMessage(string message, int times) {
    for (int i = 0; i < times; i++) {
        cout << message << endl;
    }
}

int getMax(int a, int b, int c) {
    int max = a;
    if (b > max) max = b;
    if (c > max) max = c;
    return max;
}
```

## 2. Function Parameters

### Pass by Value
```cpp
#include <iostream>
using namespace std;

// Pass by value (creates copy)
void incrementByValue(int x) {
    x++;
    cout << "Inside function (by value): " << x << endl;
}

// Pass by reference (works on original)
void incrementByReference(int &x) {
    x++;
    cout << "Inside function (by reference): " << x << endl;
}

// Pass by pointer
void incrementByPointer(int *x) {
    (*x)++;
    cout << "Inside function (by pointer): " << *x << endl;
}

int main() {
    int num = 10;
    
    cout << "Original value: " << num << endl;
    
    incrementByValue(num);
    cout << "After pass by value: " << num << endl;
    
    incrementByReference(num);
    cout << "After pass by reference: " << num << endl;
    
    incrementByPointer(&num);
    cout << "After pass by pointer: " << num << endl;
    
    return 0;
}
```

### Multiple Parameter Types
```cpp
#include <iostream>
using namespace std;

// Function with different parameter types
void processData(int integer, double decimal, string text, bool flag) {
    cout << "Integer: " << integer << endl;
    cout << "Decimal: " << decimal << endl;
    cout << "Text: " << text << endl;
    cout << "Flag: " << boolalpha << flag << endl;
}

// Function with array parameter
void printArray(int arr[], int size) {
    cout << "Array elements: ";
    for (int i = 0; i < size; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;
}

// Function modifying array elements
void doubleArrayElements(int arr[], int size) {
    for (int i = 0; i < size; i++) {
        arr[i] *= 2;
    }
}

int main() {
    // Call with different data types
    processData(42, 3.14, "Hello", true);
    
    // Array example
    int numbers[] = {1, 2, 3, 4, 5};
    int size = 5;
    
    cout << "\nOriginal array:" << endl;
    printArray(numbers, size);
    
    doubleArrayElements(numbers, size);
    
    cout << "After doubling:" << endl;
    printArray(numbers, size);
    
    return 0;
}
```

## 3. Return Types and Values

### Different Return Types
```cpp
#include <iostream>
#include <string>
#include <cmath>
using namespace std;

// Returning different data types
int getInteger() {
    return 42;
}

double getDouble() {
    return 3.14159;
}

string getString() {
    return "Hello from function!";
}

bool isEven(int number) {
    return number % 2 == 0;
}

// Returning multiple values using reference parameters
void calculateStats(double arr[], int size, double &min, double &max, double &avg) {
    min = arr[0];
    max = arr[0];
    double sum = 0;
    
    for (int i = 0; i < size; i++) {
        if (arr[i] < min) min = arr[i];
        if (arr[i] > max) max = arr[i];
        sum += arr[i];
    }
    
    avg = sum / size;
}

// Returning struct
struct Point {
    double x;
    double y;
};

Point createPoint(double x, double y) {
    Point p;
    p.x = x;
    p.y = y;
    return p;
}

int main() {
    // Basic return types
    cout << "Integer: " << getInteger() << endl;
    cout << "Double: " << getDouble() << endl;
    cout << "String: " << getString() << endl;
    cout << "Is 7 even? " << isEven(7) << endl;
    
    // Multiple return values
    double data[] = {1.5, 2.7, 3.1, 4.8, 2.2};
    double minVal, maxVal, avgVal;
    
    calculateStats(data, 5, minVal, maxVal, avgVal);
    
    cout << "\nStatistics:" << endl;
    cout << "Minimum: " << minVal << endl;
    cout << "Maximum: " << maxVal << endl;
    cout << "Average: " << avgVal << endl;
    
    // Returning struct
    Point p = createPoint(3.5, 7.2);
    cout << "\nPoint coordinates: (" << p.x << ", " << p.y << ")" << endl;
    
    return 0;
}
```

## 4. Function Overloading

### Basic Function Overloading
```cpp
#include <iostream>
using namespace std;

// Function overloading - same name, different parameters

// Version 1: Add two integers
int add(int a, int b) {
    cout << "Adding two integers: ";
    return a + b;
}

// Version 2: Add three integers
int add(int a, int b, int c) {
    cout << "Adding three integers: ";
    return a + b + c;
}

// Version 3: Add two doubles
double add(double a, double b) {
    cout << "Adding two doubles: ";
    return a + b;
}

// Version 4: Add two strings
string add(string a, string b) {
    cout << "Concatenating strings: ";
    return a + b;
}

// Version 5: Add array elements
int add(int arr[], int size) {
    cout << "Summing array elements: ";
    int sum = 0;
    for (int i = 0; i < size; i++) {
        sum += arr[i];
    }
    return sum;
}

int main() {
    // Different function calls based on parameters
    cout << add(5, 3) << endl;
    cout << add(5, 3, 2) << endl;
    cout << add(2.5, 3.7) << endl;
    cout << add("Hello", " World") << endl;
    
    int numbers[] = {1, 2, 3, 4, 5};
    cout << add(numbers, 5) << endl;
    
    return 0;
}
```

## 5. Default Arguments

### Functions with Default Parameters
```cpp
#include <iostream>
using namespace std;

// Function with default arguments
void display(string message = "Hello", int times = 1, char separator = ' ') {
    for (int i = 0; i < times; i++) {
        cout << message;
        if (i < times - 1) {
            cout << separator;
        }
    }
    cout << endl;
}

// Calculator with default operation
double calculate(double a, double b, char operation = '+') {
    switch (operation) {
        case '+':
            return a + b;
        case '-':
            return a - b;
        case '*':
            return a * b;
        case '/':
            if (b != 0) return a / b;
            else {
                cout << "Error: Division by zero!" << endl;
                return 0;
            }
        default:
            cout << "Error: Invalid operation!" << endl;
            return 0;
    }
}

// Important: Default arguments must be at the end
void printInfo(string name, int age = 0, string city = "Unknown") {
    cout << "Name: " << name << endl;
    cout << "Age: " << age << endl;
    cout << "City: " << city << endl;
}

int main() {
    // Using default arguments
    display();                          // Uses all defaults
    display("Hi");                      // Uses default times and separator
    display("C++", 3);                  // Uses default separator
    display("Awesome", 2, '|');         // Uses all provided values
    
    cout << endl;
    
    // Calculator with default operation
    cout << "5 + 3 = " << calculate(5, 3) << endl;          // Default addition
    cout << "5 - 3 = " << calculate(5, 3, '-') << endl;
    cout << "5 * 3 = " << calculate(5, 3, '*') << endl;
    cout << "5 / 3 = " << calculate(5, 3, '/') << endl;
    
    cout << endl;
    
    // Person info with defaults
    printInfo("Alice");
    printInfo("Bob", 25);
    printInfo("Charlie", 30, "New York");
    
    return 0;
}
```

## 6. Inline Functions

### Using Inline Functions
```cpp
#include <iostream>
using namespace std;

// Inline function - suggests compiler to insert code directly
inline int square(int x) {
    return x * x;
}

inline int cube(int x) {
    return x * x * x;
}

inline bool isPositive(int x) {
    return x > 0;
}

inline int getMax(int a, int b) {
    return (a > b) ? a : b;
}

// Not suitable for inline (too complex)
int factorial(int n) {
    if (n <= 1) return 1;
    return n * factorial(n - 1);
}

int main() {
    int num = 5;
    
    cout << "Number: " << num << endl;
    cout << "Square: " << square(num) << endl;
    cout << "Cube: " << cube(num) << endl;
    cout << "Is positive: " << boolalpha << isPositive(num) << endl;
    cout << "Max of " << num << " and 10: " << getMax(num, 10) << endl;
    
    // Inline functions are good for small, frequently used functions
    cout << "\nUsing inline in loop:" << endl;
    for (int i = 1; i <= 5; i++) {
        cout << "square(" << i << ") = " << square(i) << endl;
    }
    
    return 0;
}
```

## 7. Recursive Functions

### Basic Recursion Examples
```cpp
#include <iostream>
using namespace std;

// Recursive factorial
unsigned long long factorial(int n) {
    // Base case
    if (n <= 1) {
        return 1;
    }
    // Recursive case
    return n * factorial(n - 1);
}

// Recursive Fibonacci
long long fibonacci(int n) {
    // Base cases
    if (n <= 0) return 0;
    if (n == 1) return 1;
    
    // Recursive case
    return fibonacci(n - 1) + fibonacci(n - 2);
}

// Recursive power function
double power(double base, int exponent) {
    // Base case
    if (exponent == 0) return 1;
    if (exponent == 1) return base;
    
    // Handle negative exponents
    if (exponent < 0) {
        return 1 / power(base, -exponent);
    }
    
    // Recursive case for positive exponents
    return base * power(base, exponent - 1);
}

// Recursive sum of digits
int sumOfDigits(int number) {
    // Base case
    if (number == 0) return 0;
    
    // Recursive case
    return (number % 10) + sumOfDigits(number / 10);
}

// Recursive GCD (Greatest Common Divisor)
int gcd(int a, int b) {
    // Base case
    if (b == 0) return a;
    
    // Recursive case
    return gcd(b, a % b);
}

int main() {
    // Factorial examples
    cout << "Factorials:" << endl;
    for (int i = 0; i <= 10; i++) {
        cout << i << "! = " << factorial(i) << endl;
    }
    
    // Fibonacci examples
    cout << "\nFibonacci sequence:" << endl;
    for (int i = 0; i <= 10; i++) {
        cout << "F(" << i << ") = " << fibonacci(i) << endl;
    }
    
    // Power examples
    cout << "\nPower calculations:" << endl;
    cout << "2^5 = " << power(2, 5) << endl;
    cout << "3^4 = " << power(3, 4) << endl;
    cout << "5^-2 = " << power(5, -2) << endl;
    
    // Sum of digits
    cout << "\nSum of digits:" << endl;
    cout << "Sum of digits in 12345: " << sumOfDigits(12345) << endl;
    cout << "Sum of digits in 987: " << sumOfDigits(987) << endl;
    
    // GCD examples
    cout << "\nGCD calculations:" << endl;
    cout << "GCD(48, 18) = " << gcd(48, 18) << endl;
    cout << "GCD(1071, 462) = " << gcd(1071, 462) << endl;
    
    return 0;
}
```

## 8. Function Templates

### Template Functions
```cpp
#include <iostream>
using namespace std;

// Template function for finding maximum
template <typename T>
T getMax(T a, T b) {
    return (a > b) ? a : b;
}

// Template function for swapping
template <typename T>
void swapValues(T &a, T &b) {
    T temp = a;
    a = b;
    b = temp;
}

// Template function for printing array
template <typename T, int size>
void printArray(T arr[]) {
    for (int i = 0; i < size; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;
}

// Template with multiple types
template <typename T1, typename T2>
void printPair(T1 first, T2 second) {
    cout << "First: " << first << ", Second: " << second << endl;
}

// Template for linear search
template <typename T>
int linearSearch(T arr[], int size, T key) {
    for (int i = 0; i < size; i++) {
        if (arr[i] == key) {
            return i;
        }
    }
    return -1;
}

int main() {
    // Using template with different types
    cout << "Max of integers: " << getMax(5, 3) << endl;
    cout << "Max of doubles: " << getMax(2.5, 3.7) << endl;
    cout << "Max of characters: " << getMax('x', 'y') << endl;
    
    // Swapping different types
    int a = 5, b = 10;
    cout << "\nBefore swap: a = " << a << ", b = " << b << endl;
    swapValues(a, b);
    cout << "After swap: a = " << a << ", b = " << b << endl;
    
    double x = 1.5, y = 2.5;
    cout << "Before swap: x = " << x << ", y = " << y << endl;
    swapValues(x, y);
    cout << "After swap: x = " << x << ", y = " << y << endl;
    
    // Printing arrays of different types
    int intArr[] = {1, 2, 3, 4, 5};
    double doubleArr[] = {1.1, 2.2, 3.3, 4.4, 5.5};
    char charArr[] = {'A', 'B', 'C', 'D', 'E'};
    
    cout << "\nInteger array: ";
    printArray<int, 5>(intArr);
    
    cout << "Double array: ";
    printArray<double, 5>(doubleArr);
    
    cout << "Character array: ";
    printArray<char, 5>(charArr);
    
    // Multiple type parameters
    cout << "\nPairs:" << endl;
    printPair(25, "years old");
    printPair(3.14, "is pi");
    printPair("Score", 100);
    
    // Template search
    int searchArr[] = {10, 20, 30, 40, 50};
    int key = 30;
    int position = linearSearch(searchArr, 5, key);
    cout << "\nElement " << key << " found at position: " << position << endl;
    
    return 0;
}
```

## 9. Lambda Functions (C++11 and later)

### Lambda Expressions
```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    // Basic lambda syntax: [capture](parameters) -> return_type { body }
    
    // Simple lambda without parameters
    auto greet = []() {
        cout << "Hello from lambda!" << endl;
    };
    greet();
    
    // Lambda with parameters
    auto add = [](int a, int b) {
        return a + b;
    };
    cout << "5 + 3 = " << add(5, 3) << endl;
    
    // Lambda with explicit return type
    auto divide = [](double a, double b) -> double {
        if (b == 0) return 0;
        return a / b;
    };
    cout << "10 / 3 = " << divide(10, 3) << endl;
    
    // Capturing variables
    int multiplier = 5;
    
    // Capture by value [multiplier]
    auto times = [multiplier](int x) {
        return x * multiplier;
    };
    cout << "5 * 4 = " << times(4) << endl;
    
    // Capture by reference [&multiplier]
    auto incrementMultiplier = [&multiplier]() {
        multiplier++;
    };
    cout << "Before increment: " << multiplier << endl;
    incrementMultiplier();
    cout << "After increment: " << multiplier << endl;
    
    // Using lambdas with STL algorithms
    vector<int> numbers = {5, 2, 8, 1, 9, 3};
    
    cout << "\nOriginal numbers: ";
    for (int num : numbers) {
        cout << num << " ";
    }
    cout << endl;
    
    // Sort using lambda
    sort(numbers.begin(), numbers.end(), [](int a, int b) {
        return a < b;
    });
    
    cout << "Sorted numbers: ";
    for (int num : numbers) {
        cout << num << " ";
    }
    cout << endl;
    
    // Filter even numbers using lambda
    vector<int> evenNumbers;
    copy_if(numbers.begin(), numbers.end(), back_inserter(evenNumbers),
            [](int x) { return x % 2 == 0; });
    
    cout << "Even numbers: ";
    for (int num : evenNumbers) {
        cout << num << " ";
    }
    cout << endl;
    
    // Transform using lambda
    vector<int> squaredNumbers;
    transform(numbers.begin(), numbers.end(), back_inserter(squaredNumbers),
              [](int x) { return x * x; });
    
    cout << "Squared numbers: ";
    for (int num : squaredNumbers) {
        cout << num << " ";
    }
    cout << endl;
    
    return 0;
}
```

## 10. Function Pointers and std::function

### Function Pointers
```cpp
#include <iostream>
#include <functional>  // for std::function
#include <vector>
#include <cmath>
using namespace std;

// Regular functions
int add(int a, int b) {
    return a + b;
}

int subtract(int a, int b) {
    return a - b;
}

int multiply(int a, int b) {
    return a * b;
}

double squareRoot(double x) {
    return sqrt(x);
}

void printMessage(string message) {
    cout << "Message: " << message << endl;
}

// Function that takes function pointer as parameter
void calculate(int a, int b, int (*operation)(int, int)) {
    int result = operation(a, b);
    cout << "Result: " << result << endl;
}

// Using std::function
void processNumber(double x, function<double(double)> func) {
    double result = func(x);
    cout << "Processed result: " << result << endl;
}

int main() {
    // Function pointer declaration
    int (*funcPtr)(int, int);
    
    // Assign function to pointer
    funcPtr = add;
    cout << "Using function pointer - Addition: " << funcPtr(5, 3) << endl;
    
    funcPtr = subtract;
    cout << "Using function pointer - Subtraction: " << funcPtr(5, 3) << endl;
    
    funcPtr = multiply;
    cout << "Using function pointer - Multiplication: " << funcPtr(5, 3) << endl;
    
    // Array of function pointers
    int (*operations[])(int, int) = {add, subtract, multiply};
    string operationNames[] = {"Addition", "Subtraction", "Multiplication"};
    
    cout << "\nUsing array of function pointers:" << endl;
    for (int i = 0; i < 3; i++) {
        cout << operationNames[i] << ": " << operations[i](10, 4) << endl;
    }
    
    // Passing function pointer as argument
    cout << "\nPassing function pointers:" << endl;
    calculate(8, 2, add);
    calculate(8, 2, subtract);
    calculate(8, 2, multiply);
    
    // Using std::function
    cout << "\nUsing std::function:" << endl;
    function<double(double)> mathFunc;
    
    mathFunc = squareRoot;
    processNumber(16.0, mathFunc);
    
    // Lambda with std::function
    mathFunc = [](double x) { return x * x; };
    processNumber(5.0, mathFunc);
    
    mathFunc = [](double x) { return sin(x); };
    processNumber(3.14159 / 2, mathFunc);
    
    // Vector of std::function
    vector<function<void(string)>> messageFunctions;
    messageFunctions.push_back(printMessage);
    messageFunctions.push_back([](string msg) { 
        cout << "Lambda: " << msg << endl; 
    });
    
    cout << "\nVector of functions:" << endl;
    for (auto& func : messageFunctions) {
        func("Hello from function vector!");
    }
    
    return 0;
}
```

## 11. Complete Practical Example: Banking System

```cpp
#include <iostream>
#include <vector>
#include <string>
#include <iomanip>
using namespace std;

struct Account {
    int accountNumber;
    string holderName;
    double balance;
};

// Function declarations
void displayMenu();
void createAccount(vector<Account> &accounts);
void deposit(vector<Account> &accounts, int accountNumber, double amount);
void withdraw(vector<Account> &accounts, int accountNumber, double amount);
void displayAccount(const vector<Account> &accounts, int accountNumber);
void displayAllAccounts(const vector<Account> &accounts);
int findAccount(const vector<Account> &accounts, int accountNumber);
double calculateTotalBalance(const vector<Account> &accounts);
void applyInterest(vector<Account> &accounts, double rate);

int main() {
    vector<Account> accounts;
    int choice;
    
    do {
        displayMenu();
        cout << "Enter your choice: ";
        cin >> choice;
        
        switch (choice) {
            case 1: {
                createAccount(accounts);
                break;
            }
            case 2: {
                int accNumber;
                double amount;
                cout << "Enter account number: ";
                cin >> accNumber;
                cout << "Enter deposit amount: $";
                cin >> amount;
                deposit(accounts, accNumber, amount);
                break;
            }
            case 3: {
                int accNumber;
                double amount;
                cout << "Enter account number: ";
                cin >> accNumber;
                cout << "Enter withdrawal amount: $";
                cin >> amount;
                withdraw(accounts, accNumber, amount);
                break;
            }
            case 4: {
                int accNumber;
                cout << "Enter account number: ";
                cin >> accNumber;
                displayAccount(accounts, accNumber);
                break;
            }
            case 5: {
                displayAllAccounts(accounts);
                break;
            }
            case 6: {
                double total = calculateTotalBalance(accounts);
                cout << fixed << setprecision(2);
                cout << "Total bank balance: $" << total << endl;
                break;
            }
            case 7: {
                double rate;
                cout << "Enter interest rate (%): ";
                cin >> rate;
                applyInterest(accounts, rate);
                break;
            }
            case 8: {
                cout << "Thank you for using the banking system!" << endl;
                break;
            }
            default: {
                cout << "Invalid choice! Please try again." << endl;
            }
        }
        
        cout << endl;
    } while (choice != 8);
    
    return 0;
}

// Function definitions
void displayMenu() {
    cout << "=== Banking System ===" << endl;
    cout << "1. Create Account" << endl;
    cout << "2. Deposit" << endl;
    cout << "3. Withdraw" << endl;
    cout << "4. Display Account" << endl;
    cout << "5. Display All Accounts" << endl;
    cout << "6. Total Bank Balance" << endl;
    cout << "7. Apply Interest" << endl;
    cout << "8. Exit" << endl;
}

void createAccount(vector<Account> &accounts) {
    Account newAccount;
    
    cout << "Enter account number: ";
    cin >> newAccount.accountNumber;
    
    // Check if account already exists
    if (findAccount(accounts, newAccount.accountNumber) != -1) {
        cout << "Error: Account number already exists!" << endl;
        return;
    }
    
    cout << "Enter account holder name: ";
    cin.ignore();
    getline(cin, newAccount.holderName);
    
    cout << "Enter initial deposit: $";
    cin >> newAccount.balance;
    
    accounts.push_back(newAccount);
    cout << "Account created successfully!" << endl;
}

void deposit(vector<Account> &accounts, int accountNumber, double amount) {
    int index = findAccount(accounts, accountNumber);
    
    if (index == -1) {
        cout << "Error: Account not found!" << endl;
        return;
    }
    
    if (amount <= 0) {
        cout << "Error: Deposit amount must be positive!" << endl;
        return;
    }
    
    accounts[index].balance += amount;
    cout << "Deposit successful! New balance: $" << accounts[index].balance << endl;
}

void withdraw(vector<Account> &accounts, int accountNumber, double amount) {
    int index = findAccount(accounts, accountNumber);
    
    if (index == -1) {
        cout << "Error: Account not found!" << endl;
        return;
    }
    
    if (amount <= 0) {
        cout << "Error: Withdrawal amount must be positive!" << endl;
        return;
    }
    
    if (accounts[index].balance < amount) {
        cout << "Error: Insufficient funds!" << endl;
        return;
    }
    
    accounts[index].balance -= amount;
    cout << "Withdrawal successful! New balance: $" << accounts[index].balance << endl;
}

void displayAccount(const vector<Account> &accounts, int accountNumber) {
    int index = findAccount(accounts, accountNumber);
    
    if (index == -1) {
        cout << "Error: Account not found!" << endl;
        return;
    }
    
    const Account &acc = accounts[index];
    cout << fixed << setprecision(2);
    cout << "Account Number: " << acc.accountNumber << endl;
    cout << "Holder Name: " << acc.holderName << endl;
    cout << "Balance: $" << acc.balance << endl;
}

void displayAllAccounts(const vector<Account> &accounts) {
    if (accounts.empty()) {
        cout << "No accounts to display." << endl;
        return;
    }
    
    cout << fixed << setprecision(2);
    cout << setw(15) << "Account Number" << setw(20) << "Holder Name" 
         << setw(15) << "Balance" << endl;
    cout << string(50, '-') << endl;
    
    for (const Account &acc : accounts) {
        cout << setw(15) << acc.accountNumber << setw(20) << acc.holderName 
             << setw(15) << acc.balance << endl;
    }
}

int findAccount(const vector<Account> &accounts, int accountNumber) {
    for (int i = 0; i < accounts.size(); i++) {
        if (accounts[i].accountNumber == accountNumber) {
            return i;
        }
    }
    return -1;
}

double calculateTotalBalance(const vector<Account> &accounts) {
    double total = 0;
    for (const Account &acc : accounts) {
        total += acc.balance;
    }
    return total;
}

void applyInterest(vector<Account> &accounts, double rate) {
    if (rate <= 0) {
        cout << "Error: Interest rate must be positive!" << endl;
        return;
    }
    
    double interestFactor = 1 + (rate / 100.0);
    
    for (Account &acc : accounts) {
        acc.balance *= interestFactor;
    }
    
    cout << "Interest applied successfully!" << endl;
}
```
