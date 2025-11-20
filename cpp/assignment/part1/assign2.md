### **Assignment 2: Aerospace Engineering - Rocket Thrust-to-Weight Ratio**

**Objective:** Practice logical operators and conditional statements.

**Problem:**
For a rocket to lift off, its thrust must be greater than its weight. Furthermore, for a stable ascent, the Thrust-to-Weight Ratio (TWR) should be greater than 1.2. Write a program that:
1.  Asks for the rocket's thrust (in Newtons) and mass (in kg).
2.  Calculates the weight (Weight = mass * 9.81).
3.  Calculates the TWR (TWR = Thrust / Weight).
4.  Determines and prints the status:
    -   If TWR < 1: "Lift-off NOT possible."
    -   If TWR >= 1 and TWR < 1.2: "Lift-off possible, but ascent is unstable."
    -   If TWR >= 1.2: "Lift-off possible and ascent is stable."

**Expected Output:**
```
Rocket Thrust-to-Weight Ratio Analyzer
Enter rocket thrust (N): 15000
Enter rocket mass (kg): 1200
TWR: 1.274
Status: Lift-off possible and ascent is stable.
```

**Solution:**
<details> <summary>Solution</summary>

```cpp
#include <iostream>
#include <iomanip> // for setprecision
using namespace std;

int main() {
    double thrust, mass, weight, twr;

    cout << "Rocket Thrust-to-Weight Ratio Analyzer" << endl;
    cout << "Enter rocket thrust (N): ";
    cin >> thrust;
    cout << "Enter rocket mass (kg): ";
    cin >> mass;

    weight = mass * 9.81;
    twr = thrust / weight;

    cout << fixed << setprecision(3);
    cout << "TWR: " << twr << endl;
    cout << "Status: ";

    if (twr < 1) {
        cout << "Lift-off NOT possible." << endl;
    } else if (twr < 1.2) {
        cout << "Lift-off possible, but ascent is unstable." << endl;
    } else {
        cout << "Lift-off possible and ascent is stable." << endl;
    }
    return 0;
}
```

</details>