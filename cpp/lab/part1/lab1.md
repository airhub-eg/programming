### **Lab 1: Beam Load Calculator**

**Objective:** Practice basic I/O, variables, and arithmetic operations.

**Problem:**
A civil engineer needs to calculate the maximum bending moment (M) at the center of a simply supported beam with a uniformly distributed load (UDL). The formula is:
`M = (w * L^2) / 8`
Where:
- `w` is the load per unit length (in kN/m)
- `L` is the length of the beam (in meters)

Write a program that asks the user for the values of `w` and `L` and calculates the bending moment.

**Expected Output:**
```
Beam Bending Moment Calculator
Enter the load per unit length (w in kN/m): 5
Enter the beam length (L in m): 8
The maximum bending moment is: 40 kNm
```

**Solution:**
<details> <summary>Solution</summary>

```cpp
#include <iostream>
using namespace std;

int main() {
    double w, L, M;

    cout << "Beam Bending Moment Calculator" << endl;
    cout << "Enter the load per unit length (w in kN/m): ";
    cin >> w;
    cout << "Enter the beam length (L in m): ";
    cin >> L;

    M = (w * L * L) / 8;

    cout << "The maximum bending moment is: " << M << " kNm" << endl;
    return 0;
}
```

</details>