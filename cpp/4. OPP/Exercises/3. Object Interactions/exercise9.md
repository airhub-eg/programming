# Exercise 9: Distance Calculator
Create a `Point` class with:
- Private members: x, y coordinates
- Constructor
- Method `distanceFrom(Point other)` to calculate distance from another point
- Method `midpoint(Point other)` to find midpoint between two points
- Method `displayCoordinates()`
- Create multiple points and calculate distances between them

**Solution:**
<details> <summary>Solution</summary>

```cpp
#include <iostream>
#include <cmath>
using namespace std;

class Point {
private:
    double x;
    double y;

public:
    // Constructor
    Point(double xCoord = 0.0, double yCoord = 0.0) {
        x = xCoord;
        y = yCoord;
    }

    // Getters
    double getX() {
        return x;
    }

    double getY() {
        return y;
    }

    // Calculate distance from another point
    double distanceFrom(Point other) {
        double dx = x - other.x;
        double dy = y - other.y;
        return sqrt(dx * dx + dy * dy);
    }

    // Find midpoint between two points
    Point midpoint(Point other) {
        double midX = (x + other.x) / 2.0;
        double midY = (y + other.y) / 2.0;
        return Point(midX, midY);
    }

    // Display coordinates
    void displayCoordinates() {
        cout << "(" << x << ", " << y << ")";
    }
};

int main() {
    // Create multiple points
    Point p1(3.0, 4.0);
    Point p2(7.0, 1.0);
    Point p3(0.0, 0.0);  // Origin
    Point p4(-2.0, 5.0);

    // Display all points
    cout << "========== POINTS ==========" << endl;
    cout << "Point 1: ";
    p1.displayCoordinates();
    cout << endl;
    
    cout << "Point 2: ";
    p2.displayCoordinates();
    cout << endl;
    
    cout << "Point 3 (Origin): ";
    p3.displayCoordinates();
    cout << endl;
    
    cout << "Point 4: ";
    p4.displayCoordinates();
    cout << endl;

    // Calculate distances
    cout << "\n========== DISTANCES ==========" << endl;
    cout << "Distance from Point 1 to Point 2: " 
         << p1.distanceFrom(p2) << endl;
    
    cout << "Distance from Point 1 to Origin: " 
         << p1.distanceFrom(p3) << endl;
    
    cout << "Distance from Point 2 to Point 4: " 
         << p2.distanceFrom(p4) << endl;
    
    cout << "Distance from Point 3 to Point 4: " 
         << p3.distanceFrom(p4) << endl;

    // Calculate midpoints
    cout << "\n========== MIDPOINTS ==========" << endl;
    
    Point mid1 = p1.midpoint(p2);
    cout << "Midpoint between Point 1 and Point 2: ";
    mid1.displayCoordinates();
    cout << endl;
    
    Point mid2 = p3.midpoint(p4);
    cout << "Midpoint between Origin and Point 4: ";
    mid2.displayCoordinates();
    cout << endl;
    
    Point mid3 = p1.midpoint(p3);
    cout << "Midpoint between Point 1 and Origin: ";
    mid3.displayCoordinates();
    cout << endl;

    // Create a triangle and calculate perimeter
    cout << "\n========== TRIANGLE PERIMETER ==========" << endl;
    Point a(0, 0);
    Point b(3, 0);
    Point c(0, 4);
    
    double side1 = a.distanceFrom(b);
    double side2 = b.distanceFrom(c);
    double side3 = c.distanceFrom(a);
    double perimeter = side1 + side2 + side3;
    
    cout << "Triangle vertices: ";
    a.displayCoordinates();
    cout << ", ";
    b.displayCoordinates();
    cout << ", ";
    c.displayCoordinates();
    cout << endl;
    
    cout << "Side 1 length: " << side1 << endl;
    cout << "Side 2 length: " << side2 << endl;
    cout << "Side 3 length: " << side3 << endl;
    cout << "Perimeter: " << perimeter << endl;

    return 0;
}
```

</details>