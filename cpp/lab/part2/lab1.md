### **Lab 1: Material Stress-Strain Data Table**

**Objective:** Use a `for` loop to print a table of engineering stress values for corresponding strain values, simulating a simple material test.

**Problem:**
Write a program that prints a stress-strain table. Assume a linear elastic material with a Young's Modulus (E) of 200 GPa. The program should calculate stress (σ) for strain (ε) values from 0.000 to 0.005 in steps of 0.001, using the formula:
**σ = E * ε**

Print the results in a clean, two-column table.

**Expected Output:**
```
Strain (%)   Stress (MPa)
-----------------------
0.000        0.0
0.001        200.0
0.002        400.0
0.003        600.0
0.004        800.0
0.005        1000.0
```

**Solution:**
<details> <summary>Solution</summary>

```cpp
#include <iostream>
#include <iomanip>
using namespace std;

int main() {
    const double youngModulus = 200000; // MPa (200 GPa = 200,000 MPa)
    
    cout << "Strain (%)   Stress (MPa)" << endl;
    cout << "-----------------------" << endl;
    
    cout << fixed << setprecision(3);
    for (double strain = 0.000; strain <= 0.005; strain += 0.001) {
        double stress = youngModulus * strain;
        cout << strain << "        " << setw(8) << stress << endl;
    }
    
    return 0;
}
```

</details>