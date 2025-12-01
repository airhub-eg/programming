### Exercise 3: Rectangle Class
Create a `Rectangle` class with:
- Private members: length, width
- Constructor
- Methods: `calculateArea()`, `calculatePerimeter()`, `isSquare()`
- Getters and setters with validation (no negative values)
- Create multiple rectangles and test all methods

**Solution:**
<details> <summary>Solution</summary>

```cpp
#include <iostream>
using namespace std;

class Rectangle {
private:
    double length;
    double width;

public:
    // Constructor
    Rectangle(double l, double w) {
        setLength(l);
        setWidth(w);
    }

    // Setter with validation
    void setLength(double l) {
        if (l > 0) {
            length = l;
        } else {
            cout << "Length must be positive! Setting to 1." << endl;
            length = 1;
        }
    }

    void setWidth(double w) {
        if (w > 0) {
            width = w;
        } else {
            cout << "Width must be positive! Setting to 1." << endl;
            width = 1;
        }
    }

    // Getters
    double getLength() {
        return length;
    }

    double getWidth() {
        return width;
    }

    // Calculate area
    double calculateArea() {
        return length * width;
    }

    // Calculate perimeter
    double calculatePerimeter() {
        return 2 * (length + width);
    }

    // Check if square
    bool isSquare() {
        return length == width;
    }

    // Display rectangle information
    void displayInfo() {
        cout << "\n--- Rectangle Information ---" << endl;
        cout << "Length: " << length << endl;
        cout << "Width: " << width << endl;
        cout << "Area: " << calculateArea() << endl;
        cout << "Perimeter: " << calculatePerimeter() << endl;
        cout << "Is Square: " << (isSquare() ? "Yes" : "No") << endl;
    }
};

int main() {
    // Creating multiple rectangles
    Rectangle rect1(5.0, 3.0);
    Rectangle rect2(4.0, 4.0);  // This is a square
    Rectangle rect3(7.5, 2.5);

    // Display all rectangles
    rect1.displayInfo();
    rect2.displayInfo();
    rect3.displayInfo();

    // Testing validation
    cout << "\n--- Testing Validation ---" << endl;
    Rectangle rect4(-5, 3);  // Should trigger validation

    // Modifying rectangle 1
    cout << "\n--- Modifying Rectangle 1 ---" << endl;
    rect1.setLength(10);
    rect1.setWidth(10);
    rect1.displayInfo();

    return 0;
}
```

</details>