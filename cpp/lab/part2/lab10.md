### **Lab 10: Temperature Analysis with Vectors**

**Objective:** Use a vector to dynamically store and analyze temperature data.

**Problem:**
Write a program that asks the user how many temperature readings they have, then input those readings. Calculate and display the average temperature.

**Expected Output:**
```
How many temperature readings? 3
Enter temperature 0: 22.5
Enter temperature 1: 24.1
Enter temperature 2: 23.8
Average temperature: 23.47°C
```

**Solution:**
<details> <summary>Solution</summary>

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    int numReadings;
    cout << "How many temperature readings? ";
    cin >> numReadings;
    
    vector<double> temperatures;
    double total = 0.0;
    
    for (int i = 0; i < numReadings; ++i) {
        double temp;
        cout << "Enter temperature " << i << ": ";
        cin >> temp;
        temperatures.push_back(temp);
        total += temp;
    }
    
    double average = total / numReadings;
    cout << "Average temperature: " << average << "°C" << endl;
    
    return 0;
}
```

</details>

