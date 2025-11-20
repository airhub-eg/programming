
### **Lab 3: Summation of Forces**

**Objective:** Use a loop to calculate the resultant force from multiple input forces.

**Problem:**
Write a program that asks the user to enter the magnitudes of 5 forces acting on a point (in Newtons). The program should then calculate and print the summation of these forces.

**Expected Output:**
```
Enter force 1 (N): 10.5
Enter force 2 (N): -5.2
Enter force 3 (N): 8.0
Enter force 4 (N): 3.7
Enter force 5 (N): -2.1
The resultant force is: 14.9 N
```

**Solution:**
<details> <summary>Solution</summary>

```cpp
#include <iostream>
using namespace std;

int main() {
    double totalForce = 0.0;
    double force;
    
    for (int i = 1; i <= 5; ++i) {
        cout << "Enter force " << i << " (N): ";
        cin >> force;
        totalForce += force;
    }
    
    cout << "The resultant force is: " << totalForce << " N" << endl;
    return 0;
}
```

</details>