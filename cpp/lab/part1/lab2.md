### **Lab 2: Resistor Color Code Decoder**

**Objective:** Practice `switch` statements and `enum`.

**Problem:**
Write a program that decodes the 4-band resistor color code. The user will enter four characters representing the colors (e.g., 'b' for black, 'r' for red, 'o' for orange, etc.). The program should calculate and display the resistor value in ohms.

Use the standard color code:
- Black: 0, Brown: 1, Red: 2, Orange: 3, Yellow: 4, Green: 5, Blue: 6, Violet: 7, Grey: 8, White: 9

The first two bands are digits, the third is the multiplier, and the fourth is the tolerance (ignore for value calculation, but display it).

**Expected Output:**
```
Resistor Color Code Decoder
Enter the 1st band color (char): r
Enter the 2nd band color (char): e  // Let's assume 'e' for green (a simplification for this example)
Enter the 3rd band color (char): b
Enter the 4th band color (char): g
Resistor Value: 2500000 ohms +/- 5%
```

**Solution:**
<details> <summary>Solution</summary>

```cpp
#include <iostream>
using namespace std;

int colorToDigit(char color) {
    switch (color) {
        case 'k': return 0; // Black
        case 'n': return 1; // Brown
        case 'r': return 2; // Red
        case 'o': return 3; // Orange
        case 'y': return 4; // Yellow
        case 'g': return 5; // Green
        case 'b': return 6; // Blue
        case 'v': return 7; // Violet
        case 'e': return 8; // Grey
        case 'w': return 9; // White
        default: return -1; // Error
    }
}

int main() {
    char band1, band2, band3, band4;
    int digit1, digit2, multiplier;
    long long resistance;

    cout << "Resistor Color Code Decoder" << endl;
    cout << "Enter the 1st band color (char): ";
    cin >> band1;
    cout << "Enter the 2nd band color (char): ";
    cin >> band2;
    cout << "Enter the 3rd band color (char): ";
    cin >> band3;
    cout << "Enter the 4th band color (char): ";
    cin >> band4;

    digit1 = colorToDigit(band1);
    digit2 = colorToDigit(band2);
    multiplier = colorToDigit(band3);

    if (digit1 == -1 || digit2 == -1 || multiplier == -1) {
        cout << "Invalid color code!" << endl;
        return 1;
    }

    resistance = (digit1 * 10 + digit2);
    for (int i = 0; i < multiplier; i++) {
        resistance *= 10;
    }

    cout << "Resistor Value: " << resistance << " ohms" << endl;
    // A more complete solution would also decode the tolerance from band4
    return 0;
}
```

</details>