### **Lab 2: Sensor Data Validation (Even/Odd Check)**

**Objective:** Use a loop and conditional statements to filter and validate sensor readings.

**Problem:**
A sensor collects data points, but only even-numbered readings are considered valid for a particular analysis. Write a program that prints all valid (even) sensor readings from a series of 15 simulated measurements (from 0 to 14).

**Expected Output:**
```
Valid sensor readings:
0
2
4
6
8
10
12
14
```

**Solution:**
<details> <summary>Solution</summary>

```cpp
#include <iostream>
using namespace std;

int main() {
    cout << "Valid sensor readings:" << endl;
    for (int reading = 0; reading < 15; ++reading) {
        if (reading % 2 == 0) { // Check if reading is even
            cout << reading << endl;
        }
    }
    return 0;
}
```

</details>