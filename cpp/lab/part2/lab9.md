### **Lab 9: Deflection Calculation Using Arrays**

**Objective:** Use an array to store and process multiple deflection values.

**Problem:**
Write a program that asks the user to enter deflection measurements (in mm) for 5 different points on a beam. Store these in an array, then print them in reverse order.

**Expected Output:**
```
Enter deflection at point 0: 2.5
Enter deflection at point 1: 3.1
Enter deflection at point 2: 1.8
Enter deflection at point 3: 2.9
Enter deflection at point 4: 3.5
Deflections in reverse order:
3.5
2.9
1.8
3.1
2.5
```

**Solution:**
<details> <summary>Solution</summary>

```cpp
#include <iostream>
using namespace std;

int main() {
    const int numPoints = 5;
    double deflections[numPoints];
    
    for (int i = 0; i < numPoints; ++i) {
        cout << "Enter deflection at point " << i << ": ";
        cin >> deflections[i];
    }
    
    cout << "Deflections in reverse order:" << endl;
    for (int i = numPoints - 1; i >= 0; --i) {
        cout << deflections[i] << endl;
    }
    
    return 0;
}
```

</details>
