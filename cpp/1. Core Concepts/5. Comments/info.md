# Comments in C++

## Introduction to Comments
Comments are non-executable text in source code that explain the code's functionality, purpose, or design. They are ignored by the compiler but are crucial for code documentation and maintenance.

## Types of Comments in C++

### 1. Single-Line Comments (`//`)
```cpp
#include <iostream>
using namespace std;

int main() {
    // This is a single-line comment
    cout << "Hello, World!" << endl;  // Prints greeting message
    
    // Single-line comments can also be on their own line
    // They are perfect for brief explanations
    
    int age = 25;  // Variable to store user's age
    double salary = 50000.0;  // Annual salary in dollars
    
    return 0;
}
```

### 2. Multi-Line Comments (`/* */`)
```cpp
#include <iostream>
using namespace std;

/*
 * This is a multi-line comment
 * It can span across multiple lines
 * Useful for longer explanations
 */

int main() {
    /*
     * Program: Employee Management System
     * Author: John Doe
     * Date: 2024-01-15
     * Version: 1.0
     */
    
    int employeeCount = 0;  // Tracks total employees
    
    /* 
     * The following section initializes
     * employee data and calculates
     * monthly payroll
     */
    double hourlyRate = 25.50;
    double hoursWorked = 40.0;
    
    return 0;
}
```

## Commenting Best Practices

### Good Commenting Examples
```cpp
#include <iostream>
#include <cmath>
using namespace std;

/*
 * Calculator Class
 * Provides basic arithmetic operations
 * and advanced mathematical functions
 */
class Calculator {
public:
    // Adds two numbers and returns the result
    double add(double a, double b) {
        return a + b;
    }
    
    // Calculates square root using Newton's method
    // Parameters: number - must be non-negative
    // Returns: square root of the input number
    double sqrt(double number) {
        if (number < 0) {
            // Throw exception for negative input
            throw invalid_argument("Cannot calculate square root of negative number");
        }
        
        double guess = number / 2.0;
        double epsilon = 1e-10;  // Precision threshold
        
        // Iterate until convergence
        while (abs(guess * guess - number) > epsilon) {
            guess = (guess + number / guess) / 2.0;
        }
        
        return guess;
    }
};

int main() {
    Calculator calc;
    
    // Test basic arithmetic
    double result = calc.add(10.5, 20.3);
    cout << "Addition result: " << result << endl;
    
    // Test square root function
    try {
        double root = calc.sqrt(25.0);
        cout << "Square root: " << root << endl;
    } catch (const invalid_argument& e) {
        cerr << "Error: " << e.what() << endl;
    }
    
    return 0;
}
```

### Function Documentation Comments
```cpp
#include <iostream>
#include <string>
using namespace std;

/**
 * @brief Calculates the area of a rectangle
 * 
 * @param length The length of the rectangle (must be positive)
 * @param width The width of the rectangle (must be positive)
 * @return double The area of the rectangle
 * @throws invalid_argument if length or width is negative
 */
double calculateRectangleArea(double length, double width) {
    if (length <= 0 || width <= 0) {
        throw invalid_argument("Length and width must be positive");
    }
    return length * width;
}

/**
 * @brief Checks if a number is prime
 * 
 * This function uses trial division to determine if a number is prime.
 * It checks divisibility by all integers from 2 to sqrt(n).
 * 
 * @param number The number to check (must be greater than 1)
 * @return true if the number is prime
 * @return false if the number is not prime
 */
bool isPrime(int number) {
    if (number <= 1) return false;
    if (number == 2) return true;
    if (number % 2 == 0) return false;
    
    // Check odd divisors up to sqrt(number)
    for (int i = 3; i * i <= number; i += 2) {
        if (number % i == 0) {
            return false;
        }
    }
    return true;
}
```

## Different Commenting Styles

### 1. Header Comments
```cpp
/******************************************************************************
 * FILE: employee_management.cpp
 * 
 * DESCRIPTION:
 *   This program manages employee records including:
 *   - Adding new employees
 *   - Calculating payroll
 *   - Generating reports
 * 
 * AUTHOR: Jane Smith
 * DATE: 2024-01-15
 * VERSION: 2.1
 * 
 * COPYRIGHT: © 2024 Company Name. All rights reserved.
 ******************************************************************************/

#include <iostream>
#include <vector>
using namespace std;

// Rest of the code...
```

### 2. Section Comments
```cpp
#include <iostream>
#include <vector>
using namespace std;

// =============================================================================
// CONSTANT DEFINITIONS
// =============================================================================
const int MAX_EMPLOYEES = 1000;
const double TAX_RATE = 0.15;
const int MAX_WORK_HOURS = 40;

// =============================================================================
// DATA STRUCTURES
// =============================================================================
struct Employee {
    int id;
    string name;
    double salary;
    int department;
};

// =============================================================================
// FUNCTION DECLARATIONS
// =============================================================================
void addEmployee(vector<Employee>& employees);
void displayEmployees(const vector<Employee>& employees);
double calculateNetSalary(double grossSalary);

// =============================================================================
// MAIN PROGRAM
// =============================================================================
int main() {
    vector<Employee> employees;
    
    // Program logic here...
    
    return 0;
}
```

### 3. Inline Comments
```cpp
#include <iostream>
using namespace std;

int main() {
    // Initialize variables
    int count = 0;          // Loop counter
    double total = 0.0;     // Accumulator for sum
    double average = 0.0;   // Store calculated average
    
    const int SIZE = 5;     // Array size
    double numbers[SIZE];   // Array to store numbers
    
    // Input numbers
    for (int i = 0; i < SIZE; i++) {
        cout << "Enter number " << (i + 1) << ": ";
        cin >> numbers[i];
        total += numbers[i];  // Add to running total
    }
    
    // Calculate average
    average = total / SIZE;  // Division by constant is safe
    
    // Display results
    cout << "Average: " << average << endl;
    
    return 0;
}
```

## Advanced Commenting Techniques

### 1. TODO Comments
```cpp
#include <iostream>
using namespace std;

class DatabaseManager {
public:
    void connect() {
        // TODO: Implement database connection logic
        // FIXME: Currently using hardcoded credentials
        // HACK: Temporary solution for demo purposes
    }
    
    void queryData() {
        // TODO: Add error handling for network failures
        // TODO: Implement query optimization
        // NOTE: This method assumes database is already connected
    }
};

// BUG: Memory leak in destructor needs fixing
// REVIEW: Should we use smart pointers instead?
```

### 2. Debugging Comments
```cpp
#include <iostream>
using namespace std;

int factorial(int n) {
    // DEBUG: cout << "Calculating factorial of " << n << endl;
    
    if (n <= 1) {
        // DEBUG: cout << "Base case reached, returning 1" << endl;
        return 1;
    }
    
    int result = n * factorial(n - 1);
    // DEBUG: cout << "Factorial(" << n << ") = " << result << endl;
    
    return result;
}

int main() {
    // Temporary debugging code
    /*
    cout << "Debugging output:" << endl;
    for (int i = 0; i < 5; i++) {
        cout << "i = " << i << endl;
    }
    */
    
    int result = factorial(5);
    cout << "Final result: " << result << endl;
    
    return 0;
}
```

### 3. Conditional Compilation with Comments
```cpp
#include <iostream>
using namespace std;

#define DEBUG_MODE 1
#define LOGGING_ENABLED 0

int main() {
    int x = 10, y = 20;
    
#if DEBUG_MODE
    // Debugging information
    cout << "DEBUG: x = " << x << ", y = " << y << endl;
#endif
    
#if LOGGING_ENABLED
    // Log operations
    cout << "LOG: Operation started" << endl;
#else
    // Alternative implementation when logging is disabled
    // cout << "Logging is disabled" << endl;
#endif
    
    int result = x + y;
    
    // Commented-out alternative implementation
    /*
    int result = x * y;  // Alternative: multiplication instead of addition
    cout << "Product: " << result << endl;
    */
    
    cout << "Sum: " << result << endl;
    
    return 0;
}
```

## Doxygen Documentation Comments

```cpp
/**
 * @file calculator.h
 * @brief A comprehensive calculator class for mathematical operations
 * 
 * @author John Doe
 * @date 2024-01-15
 * @version 2.0
 */

#include <iostream>
#include <cmath>
using namespace std;

/**
 * @class AdvancedCalculator
 * @brief Provides advanced mathematical operations
 * 
 * This class extends basic calculator functionality with
 * trigonometric, logarithmic, and statistical operations.
 */
class AdvancedCalculator {
private:
    double lastResult;  ///< Stores the result of the last operation
    
public:
    /**
     * @brief Constructor initializing the calculator
     * @param initialValue The starting value (default: 0)
     */
    AdvancedCalculator(double initialValue = 0) : lastResult(initialValue) {}
    
    /**
     * @brief Calculates the power of a number
     * @param base The base number
     * @param exponent The exponent
     * @return double base raised to the power of exponent
     * 
     * @code
     * AdvancedCalculator calc;
     * double result = calc.power(2, 3);  // Returns 8.0
     * @endcode
     */
    double power(double base, double exponent) {
        lastResult = pow(base, exponent);
        return lastResult;
    }
    
    /**
     * @brief Gets the last calculated result
     * @return double The result of the last operation
     */
    double getLastResult() const {
        return lastResult;
    }
    
    /**
     * @brief Resets the calculator to initial state
     */
    void reset() {
        lastResult = 0;
    }
};

/**
 * @brief Main function demonstrating calculator usage
 * @return int Exit status (0 for success)
 */
int main() {
    AdvancedCalculator calc;
    
    // Calculate 2^8
    double result = calc.power(2, 8);
    cout << "2^8 = " << result << endl;
    
    return 0;
}
```

## Commenting for Different Scenarios

### 1. Algorithm Explanation
```cpp
#include <iostream>
#include <vector>
using namespace std;

/**
 * @brief Sorts an array using bubble sort algorithm
 * 
 * Bubble sort works by repeatedly swapping adjacent elements
 * if they are in the wrong order. This process is repeated
 * until the entire array is sorted.
 * 
 * Time Complexity: O(n²)
 * Space Complexity: O(1)
 * 
 * @param arr The array to be sorted
 * @param n The size of the array
 */
void bubbleSort(int arr[], int n) {
    // Outer loop: number of passes needed
    for (int i = 0; i < n - 1; i++) {
        // Inner loop: compare adjacent elements
        for (int j = 0; j < n - i - 1; j++) {
            // Swap if current element is greater than next
            if (arr[j] > arr[j + 1]) {
                // Swap elements using temporary variable
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
        // After each pass, the largest element bubbles to the end
    }
}
```

### 2. Complex Business Logic
```cpp
#include <iostream>
using namespace std;

class LoanCalculator {
private:
    double principal;
    double annualRate;
    int years;
    
public:
    /**
     * @brief Calculates monthly mortgage payment
     * 
     * Uses the formula: 
     * M = P [ r(1+r)^n ] / [ (1+r)^n - 1 ]
     * Where:
     * M = monthly payment
     * P = principal loan amount
     * r = monthly interest rate (annual rate / 12)
     * n = total number of payments (years * 12)
     * 
     * @return double Monthly payment amount
     */
    double calculateMonthlyPayment() {
        // Convert annual rate to monthly and percentage to decimal
        double monthlyRate = (annualRate / 100) / 12;
        
        // Calculate total number of payments
        int totalPayments = years * 12;
        
        // Calculate (1+r)^n
        double compoundFactor = pow(1 + monthlyRate, totalPayments);
        
        // Apply the formula
        double monthlyPayment = principal * 
                               (monthlyRate * compoundFactor) / 
                               (compoundFactor - 1);
        
        return monthlyPayment;
    }
};
```

## Common Commenting Mistakes to Avoid

### Bad Commenting Examples
```cpp
#include <iostream>
using namespace std;

// Bad: Obvious comments
int x = 5;  // set x to 5
x = x + 1;  // increment x by 1

// Bad: Outdated comments
int oldValue = 10;  // This value should be 15 (but it was changed)

// Bad: Commented-out code without explanation
/*
void oldFunction() {
    // This doesn't work anymore
    // But we keep it just in case
}
*/

// Bad: Too many trivial comments
int main() {
    // Initialize counter
    int i = 0;
    
    // Start loop
    while (i < 10) {
        // Print number
        cout << i << endl;
        // Increment counter
        i++;
    }
    // End of program
    return 0;
}
```

### Good vs Bad Comments
```cpp
#include <iostream>
using namespace std;

// BAD: Redundant comment
int count = 0;  // initialize count to zero

// GOOD: Explains why, not what
int retryAttempts = 0;  // Maximum 3 retry attempts per protocol

// BAD: Obvious comment
void saveData() {
    // Save data to file
    ofstream file("data.txt");
    // Write data
    file << data;
    // Close file
    file.close();
}

// GOOD: Explains the purpose and any important details
void saveUserPreferences() {
    // Save user preferences in JSON format for cross-platform compatibility
    // The file is stored in app data directory for persistence
    ofstream file(getPreferencesPath());
    file << preferencesToJson();
    file.close();
}
```

## Practical Complete Example

```cpp
/******************************************************************************
 * FILE: bank_account.cpp
 * 
 * DESCRIPTION:
 *   Implements a simple bank account system with deposit, withdrawal,
 *   and balance inquiry functionality.
 * 
 * FEATURES:
 *   - Account balance management
 *   - Transaction history
 *   - Overdraft protection
 * 
 * AUTHOR: Finance Team
 * DATE: 2024-01-15
 * VERSION: 1.2
 ******************************************************************************/

#include <iostream>
#include <vector>
#include <string>
using namespace std;

// =============================================================================
// CONSTANTS AND CONFIGURATION
// =============================================================================
const double OVERDRAFT_LIMIT = -1000.00;  // Maximum allowed overdraft
const double MIN_BALANCE = 10.00;         // Minimum balance to avoid fees

// =============================================================================
// DATA STRUCTURES
// =============================================================================

/**
 * @brief Represents a single financial transaction
 */
struct Transaction {
    string date;      // Transaction date in YYYY-MM-DD format
    string type;      // "DEPOSIT", "WITHDRAWAL", or "FEE"
    double amount;    // Transaction amount (positive for deposits)
    double balance;   // Account balance after transaction
};

/**
 * @brief Manages bank account operations and balance
 */
class BankAccount {
private:
    string accountNumber;
    string accountHolder;
    double balance;
    vector<Transaction> transactionHistory;

public:
    // =========================================================================
    // CONSTRUCTOR
    // =========================================================================
    BankAccount(string accNum, string holder, double initialBalance = 0.0)
        : accountNumber(accNum), accountHolder(holder), balance(initialBalance) {
        
        // Record initial deposit if provided
        if (initialBalance > 0) {
            recordTransaction("INITIAL", "DEPOSIT", initialBalance);
        }
    }
    
    // =========================================================================
    // PUBLIC METHODS
    // =========================================================================
    
    /**
     * @brief Deposits specified amount into account
     * @param amount The amount to deposit (must be positive)
     * @return true if deposit successful, false otherwise
     */
    bool deposit(double amount) {
        // Validate input
        if (amount <= 0) {
            cerr << "ERROR: Deposit amount must be positive" << endl;
            return false;
        }
        
        // Update balance
        balance += amount;
        
        // Record transaction
        recordTransaction(getCurrentDate(), "DEPOSIT", amount);
        
        cout << "Successfully deposited: $" << amount << endl;
        return true;
    }
    
    /**
     * @brief Withdraws specified amount from account
     * 
     * Checks for sufficient funds and overdraft limits before
     * processing the withdrawal.
     * 
     * @param amount The amount to withdraw (must be positive)
     * @return true if withdrawal successful, false otherwise
     */
    bool withdraw(double amount) {
        // Validate input
        if (amount <= 0) {
            cerr << "ERROR: Withdrawal amount must be positive" << endl;
            return false;
        }
        
        // Check if withdrawal would exceed overdraft limit
        if ((balance - amount) < OVERDRAFT_LIMIT) {
            cerr << "ERROR: Insufficient funds. Overdraft limit exceeded." << endl;
            return false;
        }
        
        // Update balance
        balance -= amount;
        
        // Record transaction
        recordTransaction(getCurrentDate(), "WITHDRAWAL", amount);
        
        cout << "Successfully withdrew: $" << amount << endl;
        return true;
    }
    
    /**
     * @brief Displays current account balance
     */
    void displayBalance() const {
        cout << "Account: " << accountNumber << endl;
        cout << "Holder: " << accountHolder << endl;
        cout << "Current Balance: $" << balance << endl;
        
        // Warn if balance is below minimum
        if (balance < MIN_BALANCE) {
            cout << "WARNING: Balance below minimum required amount" << endl;
        }
    }
    
    // =========================================================================
    // PRIVATE HELPER METHODS
    // =========================================================================
private:
    /**
     * @brief Records a transaction in the history
     * @param date Transaction date
     * @param type Transaction type
     * @param amount Transaction amount
     */
    void recordTransaction(string date, string type, double amount) {
        Transaction transaction;
        transaction.date = date;
        transaction.type = type;
        transaction.amount = amount;
        transaction.balance = balance;
        
        transactionHistory.push_back(transaction);
    }
    
    /**
     * @brief Generates current date string (simplified)
     * @return string Current date in YYYY-MM-DD format
     * 
     * TODO: Replace with actual date library in production
     */
    string getCurrentDate() const {
        return "2024-01-15";  // Placeholder for demo
    }
};

// =============================================================================
// MAIN APPLICATION
// =============================================================================
int main() {
    // Create a test account
    BankAccount myAccount("123456789", "John Doe", 1000.00);
    
    // Display initial balance
    myAccount.displayBalance();
    cout << endl;
    
    // Test deposits and withdrawals
    myAccount.deposit(500.00);
    myAccount.withdraw(200.00);
    myAccount.withdraw(1500.00);  // This might fail due to overdraft
    
    cout << endl;
    myAccount.displayBalance();
    
    return 0;
}
```