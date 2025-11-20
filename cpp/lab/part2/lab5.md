### **Lab 5: Input Validation for Engineering Parameter**

**Objective:** Use a `while` loop to validate user input against engineering constraints.

**Problem:**
Write a program that asks the user to enter a safety factor. The safety factor must be greater than or equal to 1.5. If the user enters an invalid value, the program should keep asking until a valid value is provided.

**Expected Output:**
```
Enter the safety factor (must be >= 1.5): 1.2
Invalid! Enter the safety factor (must be >= 1.5): 0.9
Invalid! Enter the safety factor (must be >= 1.5): 2.0
Valid safety factor recorded: 2.0
```

**Solution:**
<details> <summary>Solution</summary>

```cpp
#include <iostream>
using namespace std;

int main() {
    double safetyFactor;
    
    cout << "Enter the safety factor (must be >= 1.5): ";
    cin >> safetyFactor;
    
    while (safetyFactor < 1.5) {
        cout << "Invalid! Enter the safety factor (must be >= 1.5): ";
        cin >> safetyFactor;
    }
    
    cout << "Valid safety factor recorded: " << safetyFactor << endl;
    return 0;
}
```

</details>

