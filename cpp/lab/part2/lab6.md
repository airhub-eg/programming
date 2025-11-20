### **Lab 6: Countdown to System Start**

**Objective:** Use a `while` loop to create a countdown sequence.

**Problem:**
Simulate a system startup countdown. Ask the user for a number to count down from. Then print the countdown to 0.

**Expected Output:**
```
Enter countdown start: 3
2
1
0
System Go!
```

**Solution:**
<details> <summary>Solution</summary>

```cpp
#include <iostream>
using namespace std;

int main() {
    int start;
    cout << "Enter countdown start: ";
    cin >> start;
    
    while (start >= 0) {
        cout << start << endl;
        start--;
    }
    cout << "System Go!" << endl;
    return 0;
}
```

</details>

