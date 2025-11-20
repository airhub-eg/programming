### **Lab 4: Resonant Frequencies**

**Objective:** Use a loop to find and print values that meet multiple conditions.

**Problem:**
In an electrical circuit, certain frequencies are critical. Write a program that prints all integers between 1 and 100 that are divisible by both **4 and 6** (simulating resonant frequencies of a system).

**Expected Output:**
```
12
24
36
48
60
72
84
96
```

**Solution:**
<details> <summary>Solution</summary>

```cpp
#include <iostream>
using namespace std;

int main() {
    cout << "Critical frequencies:" << endl;
    for (int freq = 1; freq <= 100; ++freq) {
        if (freq % 4 == 0 && freq % 6 == 0) {
            cout << freq << endl;
        }
    }
    return 0;
}
```

</details>

