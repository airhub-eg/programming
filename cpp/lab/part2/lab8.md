### **Lab 8: Password Validation for System Access**

**Objective:** Use a `do-while` loop to repeatedly ask for a password until the correct one is entered.

**Problem:**
Write a program that asks the user to enter the engineering system password ("Turbine2024"). The program should keep asking until the correct password is entered.

**Expected Output:**
```
Enter system password: hello
Access denied!
Enter system password: test
Access denied!
Enter system password: Turbine2024
Access granted!
```

**Solution:**
<details> <summary>Solution</summary>

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    const string correctPassword = "Turbine2024";
    string inputPassword;
    
    do {
        cout << "Enter system password: ";
        cin >> inputPassword;
        
        if (inputPassword != correctPassword) {
            cout << "Access denied!" << endl;
        }
    } while (inputPassword != correctPassword);
    
    cout << "Access granted!" << endl;
    return 0;
}
```

</details>

