# Conditional Statements in C++

## Introduction to Conditional Statements
Conditional statements allow programs to make decisions and execute different code blocks based on specified conditions. They are fundamental to creating dynamic, responsive programs.

## 1. The `if` Statement

### Basic `if` Statement
```cpp
#include <iostream>
using namespace std;

int main() {
    int number;
    
    cout << "Enter a number: ";
    cin >> number;
    
    // Basic if statement
    if (number > 0) {
        cout << "The number is positive." << endl;
    }
    
    // Single statement if (braces optional for single statement)
    if (number == 0)
        cout << "The number is zero." << endl;
    
    return 0;
}
```

### Multiple Conditions in `if`
```cpp
#include <iostream>
using namespace std;

int main() {
    int age;
    bool hasID;
    
    cout << "Enter your age: ";
    cin >> age;
    cout << "Do you have ID? (1 for yes, 0 for no): ";
    cin >> hasID;
    
    // Multiple conditions using logical operators
    if (age >= 18 && hasID) {
        cout << "You can enter the club." << endl;
    }
    
    if (age < 18 || !hasID) {
        cout << "Sorry, you cannot enter." << endl;
    }
    
    return 0;
}
```

## 2. The `if-else` Statement

### Basic `if-else`
```cpp
#include <iostream>
using namespace std;

int main() {
    int number;
    
    cout << "Enter a number: ";
    cin >> number;
    
    if (number % 2 == 0) {
        cout << number << " is even." << endl;
    } else {
        cout << number << " is odd." << endl;
    }
    
    return 0;
}
```

### Multiple `if-else` Statements
```cpp
#include <iostream>
using namespace std;

int main() {
    int score;
    
    cout << "Enter your test score (0-100): ";
    cin >> score;
    
    if (score >= 90) {
        cout << "Grade: A" << endl;
    } else if (score >= 80) {
        cout << "Grade: B" << endl;
    } else if (score >= 70) {
        cout << "Grade: C" << endl;
    } else if (score >= 60) {
        cout << "Grade: D" << endl;
    } else {
        cout << "Grade: F" << endl;
    }
    
    return 0;
}
```

## 3. Nested `if` Statements

```cpp
#include <iostream>
using namespace std;

int main() {
    int age;
    bool hasDriverLicense;
    bool hasParentalConsent;
    
    cout << "Enter your age: ";
    cin >> age;
    cout << "Do you have a driver's license? (1/0): ";
    cin >> hasDriverLicense;
    
    if (age >= 18) {
        if (hasDriverLicense) {
            cout << "You can drive alone." << endl;
        } else {
            cout << "You need to get a driver's license first." << endl;
        }
    } else {
        cout << "Do you have parental consent? (1/0): ";
        cin >> hasParentalConsent;
        
        if (hasParentalConsent && age >= 16) {
            cout << "You can drive with parental consent." << endl;
        } else {
            cout << "You cannot drive yet." << endl;
        }
    }
    
    return 0;
}
```

## 4. The `switch` Statement

### Basic `switch` Statement
```cpp
#include <iostream>
using namespace std;

int main() {
    int dayNumber;
    
    cout << "Enter day number (1-7): ";
    cin >> dayNumber;
    
    switch (dayNumber) {
        case 1:
            cout << "Monday" << endl;
            break;
        case 2:
            cout << "Tuesday" << endl;
            break;
        case 3:
            cout << "Wednesday" << endl;
            break;
        case 4:
            cout << "Thursday" << endl;
            break;
        case 5:
            cout << "Friday" << endl;
            break;
        case 6:
            cout << "Saturday" << endl;
            break;
        case 7:
            cout << "Sunday" << endl;
            break;
        default:
            cout << "Invalid day number!" << endl;
            break;
    }
    
    return 0;
}
```

### `switch` with Multiple Cases
```cpp
#include <iostream>
using namespace std;

int main() {
    char grade;
    
    cout << "Enter your grade (A, B, C, D, F): ";
    cin >> grade;
    
    switch (grade) {
        case 'A':
        case 'a':
            cout << "Excellent!" << endl;
            break;
        case 'B':
        case 'b':
            cout << "Good job!" << endl;
            break;
        case 'C':
        case 'c':
            cout << "Average." << endl;
            break;
        case 'D':
        case 'd':
            cout << "Needs improvement." << endl;
            break;
        case 'F':
        case 'f':
            cout << "Failed." << endl;
            break;
        default:
            cout << "Invalid grade!" << endl;
    }
    
    return 0;
}
```

### `switch` with Enum
```cpp
#include <iostream>
using namespace std;

enum TrafficLight {
    RED,
    YELLOW,
    GREEN
};

int main() {
    TrafficLight light = RED;
    
    switch (light) {
        case RED:
            cout << "Stop!" << endl;
            break;
        case YELLOW:
            cout << "Slow down!" << endl;
            break;
        case GREEN:
            cout << "Go!" << endl;
            break;
    }
    
    return 0;
}
```

## 5. Conditional (Ternary) Operator

### Basic Ternary Operator
```cpp
#include <iostream>
using namespace std;

int main() {
    int a, b;
    
    cout << "Enter two numbers: ";
    cin >> a >> b;
    
    // Ternary operator: condition ? value_if_true : value_if_false
    int max = (a > b) ? a : b;
    cout << "Maximum: " << max << endl;
    
    // Using ternary for assignment
    string result = (a == b) ? "Numbers are equal" : "Numbers are different";
    cout << result << endl;
    
    // Nested ternary operator
    int c = 15;
    string comparison = (a > b) ? 
                       ((a > c) ? "A is largest" : "C is largest") : 
                       ((b > c) ? "B is largest" : "C is largest");
    cout << comparison << endl;
    
    return 0;
}
```

## 6. Logical Operators in Conditions

### AND (`&&`), OR (`||`), NOT (`!`)
```cpp
#include <iostream>
using namespace std;

int main() {
    int age;
    bool hasTicket;
    bool hasParent;
    
    cout << "Enter age: ";
    cin >> age;
    cout << "Do you have a ticket? (1/0): ";
    cin >> hasTicket;
    cout << "Are you with a parent? (1/0): ";
    cin >> hasParent;
    
    // Complex conditions
    if ((age >= 18 && hasTicket) || (age < 18 && hasParent && hasTicket)) {
        cout << "You can enter the concert." << endl;
    } else {
        cout << "Sorry, you cannot enter." << endl;
    }
    
    // NOT operator examples
    if (!hasTicket) {
        cout << "You need to buy a ticket first." << endl;
    }
    
    // Combining multiple operators
    bool isWeekend = true;
    bool isHoliday = false;
    
    if (isWeekend || isHoliday) {
        cout << "No work today!" << endl;
    }
    
    return 0;
}
```

## 7. Complex Conditional Examples

### Student Grading System
```cpp
#include <iostream>
using namespace std;

int main() {
    int marks;
    char attendance;
    
    cout << "Enter student marks (0-100): ";
    cin >> marks;
    cout << "Is attendance satisfactory? (Y/N): ";
    cin >> attendance;
    
    // Complex grading with multiple conditions
    if (attendance == 'Y' || attendance == 'y') {
        if (marks >= 90) {
            cout << "Grade: A+ (Excellent)" << endl;
        } else if (marks >= 80) {
            cout << "Grade: A (Very Good)" << endl;
        } else if (marks >= 70) {
            cout << "Grade: B (Good)" << endl;
        } else if (marks >= 60) {
            cout << "Grade: C (Satisfactory)" << endl;
        } else if (marks >= 50) {
            cout << "Grade: D (Pass)" << endl;
        } else {
            cout << "Grade: F (Fail - Poor performance)" << endl;
        }
    } else {
        cout << "Grade: F (Fail - Poor attendance)" << endl;
    }
    
    return 0;
}
```

### Loan Eligibility System
```cpp
#include <iostream>
using namespace std;

int main() {
    int age;
    double income;
    int creditScore;
    bool employed;
    
    cout << "Loan Eligibility Check" << endl;
    cout << "Enter your age: ";
    cin >> age;
    cout << "Enter annual income: $";
    cin >> income;
    cout << "Enter credit score: ";
    cin >> creditScore;
    cout << "Are you employed? (1/0): ";
    cin >> employed;
    
    // Complex eligibility criteria
    if (age >= 21 && age <= 65) {
        if (employed) {
            if (income >= 30000) {
                if (creditScore >= 650) {
                    cout << "Congratulations! You are eligible for a loan." << endl;
                    
                    // Determine loan amount based on income and credit score
                    double loanAmount;
                    if (income >= 50000 && creditScore >= 750) {
                        loanAmount = 100000;
                    } else if (income >= 40000 && creditScore >= 700) {
                        loanAmount = 75000;
                    } else {
                        loanAmount = 50000;
                    }
                    
                    cout << "Approved loan amount: $" << loanAmount << endl;
                } else {
                    cout << "Sorry, credit score too low." << endl;
                }
            } else {
                cout << "Sorry, income requirement not met." << endl;
            }
        } else {
            cout << "Sorry, employment required." << endl;
        }
    } else {
        cout << "Sorry, age requirement not met." << endl;
    }
    
    return 0;
}
```

## 8. Short-Circuit Evaluation

```cpp
#include <iostream>
using namespace std;

bool checkCondition1() {
    cout << "Checking condition 1..." << endl;
    return false;
}

bool checkCondition2() {
    cout << "Checking condition 2..." << endl;
    return true;
}

bool checkCondition3() {
    cout << "Checking condition 3..." << endl;
    return true;
}

int main() {
    // Short-circuit with AND (&&)
    // If first condition is false, second won't be evaluated
    if (checkCondition1() && checkCondition2()) {
        cout << "Both conditions true" << endl;
    } else {
        cout << "At least one condition false" << endl;
    }
    
    cout << "---" << endl;
    
    // Short-circuit with OR (||)
    // If first condition is true, second won't be evaluated
    if (checkCondition2() || checkCondition3()) {
        cout << "At least one condition true" << endl;
    }
    
    // Practical example with pointer checking
    int* ptr = nullptr;
    int value = 10;
    
    // Safe way to check pointer before dereferencing
    if (ptr != nullptr && *ptr > 0) {
        cout << "Pointer is valid and value is positive" << endl;
    } else {
        cout << "Pointer is null or value is not positive" << endl;
    }
    
    return 0;
}
```

## 9. Common Pitfalls and Best Practices

### Common Mistakes
```cpp
#include <iostream>
using namespace std;

int main() {
    int x = 5, y = 10;
    
    // Common mistake 1: Assignment (=) instead of equality (==)
    if (x = 0) {  // Wrong! This assigns 0 to x, then checks if 0 is true
        cout << "x is zero" << endl;
    }
    
    // Correct way
    if (x == 0) {
        cout << "x is zero" << endl;
    }
    
    // Common mistake 2: Missing braces in complex if-else
    if (x > y)
        cout << "x is greater" << endl;
        cout << "This will always execute!" << endl;  // Not part of if!
    
    // Common mistake 3: Dangling else
    if (x > 0)
        if (y > 0)
            cout << "Both positive" << endl;
    else  // This else belongs to the inner if!
        cout << "x is not positive" << endl;  // Misleading!
    
    // Better with braces
    if (x > 0) {
        if (y > 0) {
            cout << "Both positive" << endl;
        }
    } else {
        cout << "x is not positive" << endl;
    }
    
    return 0;
}
```

### Best Practices Example
```cpp
#include <iostream>
using namespace std;

int main() {
    int temperature;
    bool isRaining;
    
    cout << "Enter temperature: ";
    cin >> temperature;
    cout << "Is it raining? (1/0): ";
    cin >> isRaining;
    
    // Good: Clear, readable conditions
    bool isWarm = (temperature > 20);
    bool isCold = (temperature < 10);
    
    if (isWarm && !isRaining) {
        cout << "Perfect weather for a picnic!" << endl;
    } else if (isWarm && isRaining) {
        cout << "Take an umbrella if you go out." << endl;
    } else if (isCold && !isRaining) {
        cout << "Wear a jacket." << endl;
    } else if (isCold && isRaining) {
        cout << "Stay indoors or wear warm rain gear." << endl;
    } else {
        cout << "Moderate weather." << endl;
    }
    
    // Using constants for magic numbers
    const int FREEZING_POINT = 0;
    const int BOILING_POINT = 100;
    
    if (temperature <= FREEZING_POINT) {
        cout << "Water will freeze." << endl;
    } else if (temperature >= BOILING_POINT) {
        cout << "Water will boil." << endl;
    }
    
    return 0;
}
```

## 10. Advanced Conditional Patterns

### Range Checking
```cpp
#include <iostream>
using namespace std;

int main() {
    int score;
    
    cout << "Enter test score: ";
    cin >> score;
    
    // Range checking with multiple conditions
    if (score < 0 || score > 100) {
        cout << "Invalid score! Must be between 0 and 100." << endl;
    } else if (score >= 0 && score <= 49) {
        cout << "Fail" << endl;
    } else if (score >= 50 && score <= 100) {
        cout << "Pass" << endl;
        
        // Nested range checking
        if (score >= 50 && score <= 64) {
            cout << "Grade: C" << endl;
        } else if (score >= 65 && score <= 79) {
            cout << "Grade: B" << endl;
        } else {
            cout << "Grade: A" << endl;
        }
    }
    
    return 0;
}
```

### Menu-Driven Program
```cpp
#include <iostream>
using namespace std;

int main() {
    int choice;
    double num1, num2, result;
    
    cout << "Simple Calculator" << endl;
    cout << "1. Addition" << endl;
    cout << "2. Subtraction" << endl;
    cout << "3. Multiplication" << endl;
    cout << "4. Division" << endl;
    cout << "Enter your choice (1-4): ";
    cin >> choice;
    
    cout << "Enter two numbers: ";
    cin >> num1 >> num2;
    
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
        default:
            cout << "Invalid choice!" << endl;
    }
    
    return 0;
}
```