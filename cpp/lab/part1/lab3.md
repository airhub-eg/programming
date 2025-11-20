### **Lab 3: Material Safety Check**

**Objective:** Practice `if-else` statements and relational operators.

**Problem:**
In a mechanical system, a component will fail if the applied stress exceeds the material's yield strength. Write a program that asks the user for:
1.  The applied stress (in MPa)
2.  The yield strength of the material (in MPa)

The program should then output whether the component is "SAFE" or "FAILS". Add a safety factor of 1.5. This means the component is only safe if: \
 `(Applied Stress * 1.5) < Yield Strength`.

**Expected Output:**
```
Component Safety Check
Enter the applied stress (MPa): 200
Enter the material yield strength (MPa): 400
Status: FAILS

Enter the applied stress (MPa): 200
Enter the material yield strength (MPa): 450
Status: SAFE
```

**Solution:**
<details> <summary>Solution</summary>

```cpp
#include <iostream>
using namespace std;

int main() {
    double appliedStress, yieldStrength;

    cout << "Component Safety Check" << endl;
    cout << "Enter the applied stress (MPa): ";
    cin >> appliedStress;
    cout << "Enter the material yield strength (MPa): ";
    cin >> yieldStrength;

    if ((appliedStress * 1.5) < yieldStrength) {
        cout << "Status: SAFE" << endl;
    } else {
        cout << "Status: FAILS" << endl;
    }
    return 0;
}
```

</details>