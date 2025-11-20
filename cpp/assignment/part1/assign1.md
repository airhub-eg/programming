### **Assignment 1: Reactor Concentration Calculator**

**Objective:** Practice functions and more complex calculations.

**Problem:**
In a continuously stirred-tank reactor (CSTR), the concentration of output `C_A` for a first-order reaction is given by:
`C_A = C_A0 / (1 + k * τ)`
Where:
- `C_A0` is the inlet concentration (mol/L)
- `k` is the reaction rate constant (1/s)
- `τ` (tau) is the residence time (s)

Write a program with a function `calculateConcentration` that takes these three parameters and returns `C_A`. The `main` function should get the inputs from the user and display the result.

**Expected Output:**
```
CSTR Concentration Calculator
Enter the inlet concentration, C_A0 (mol/L): 5
Enter the rate constant, k (1/s): 0.1
Enter the residence time, τ (s): 10
The output concentration is: 2.5 mol/L
```

**Solution:**
<details> <summary>Solution</summary>

```cpp
#include <iostream>
using namespace std;

double calculateConcentration(double C_A0, double k, double tau) {
    return C_A0 / (1 + k * tau);
}

int main() {
    double C_A0, k, tau, C_A;

    cout << "CSTR Concentration Calculator" << endl;
    cout << "Enter the inlet concentration, C_A0 (mol/L): ";
    cin >> C_A0;
    cout << "Enter the rate constant, k (1/s): ";
    cin >> k;
    cout << "Enter the residence time, τ (s): ";
    cin >> tau;

    C_A = calculateConcentration(C_A0, k, tau);

    cout << "The output concentration is: " << C_A << " mol/L" << endl;
    return 0;
}
```

</details>