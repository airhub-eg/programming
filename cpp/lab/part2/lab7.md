### **Lab 7: Repeated Area Calculation for Different Components**

**Objective:** Use a `do-while` loop to allow repeated calculations based on user choice.

**Problem:**
Write a program that calculates the cross-sectional area of a rectangular component. After each calculation, ask the user if they want to calculate another area.

**Expected Output:**
```
Enter height (m): 0.5
Enter width (m): 2.0
Cross-sectional area: 1.0 square meters
Calculate another? (y/n): y
Enter height (m): 1.0
Enter width (m): 3.0
Cross-sectional area: 3.0 square meters
Calculate another? (y/n): n
Goodbye!
```

**Solution:**
<details> <summary>Solution</summary>

```cpp
#include <iostream>
using namespace std;

int main() {
    char choice;
    do {
        double height, width;
        cout << "Enter height (m): ";
        cin >> height;
        cout << "Enter width (m): ";
        cin >> width;
        
        double area = height * width;
        cout << "Cross-sectional area: " << area << " square meters" << endl;
        
        cout << "Calculate another? (y/n): ";
        cin >> choice;
    } while (choice == 'y' || choice == 'Y');
    
    cout << "Goodbye!" << endl;
    return 0;
}
```

</details>

