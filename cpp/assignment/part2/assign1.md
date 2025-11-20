### **Assignment: Structural Member Classification**

**Objective:** Use strings and character processing to classify engineering members.

**Problem:**
Write a program that asks the user to enter a structural member type (e.g., "beam", "column", "truss"). Convert the input to uppercase and classify it:
- If "BEAM", print "Flexural member"
- If "COLUMN", print "Compression member"
- If "TRUSS", print "Axial force member"
- Otherwise, print "Unknown member type"

**Expected Output:**
```
Enter member type: beam
BEAM - Flexural member
```

**Solution:**
<details> <summary>Solution</summary>

```cpp
#include <iostream>
#include <string>
#include <cctype>
using namespace std;

int main() {
    string memberType;
    cout << "Enter member type: ";
    cin >> memberType;
    
    // Convert to uppercase
    for (char &c : memberType) {
        c = toupper(c);
    }
    
    cout << memberType << " - ";
    
    if (memberType == "BEAM") {
        cout << "Flexural member";
    } else if (memberType == "COLUMN") {
        cout << "Compression member";
    } else if (memberType == "TRUSS") {
        cout << "Axial force member";
    } else {
        cout << "Unknown member type";
    }
    cout << endl;
    
    return 0;
}
```

</details>