# Exercise 10: Time Class
Create a `Time` class with:
- Private members: hours, minutes, seconds
- Constructor with validation (24-hour format)
- Method `addTime(Time t)` to add two time objects
- Method `differenceInSeconds(Time t)` to find difference
- Method `displayTime()` in HH:MM:SS format
- Overload operators if you know them, otherwise use named methods

**Solution:**
<details> <summary>Solution</summary>

```cpp
#include <iostream>
#include <iomanip>
using namespace std;

class Time {
private:
    int hours;
    int minutes;
    int seconds;

    // Normalize time (handle overflow/underflow)
    void normalize() {
        if (seconds >= 60) {
            minutes += seconds / 60;
            seconds %= 60;
        }
        if (minutes >= 60) {
            hours += minutes / 60;
            minutes %= 60;
        }
        if (hours >= 24) {
            hours %= 24;
        }
    }

public:
    // Constructor with validation
    Time(int h = 0, int m = 0, int s = 0) {
        hours = (h >= 0 && h < 24) ? h : 0;
        minutes = (m >= 0 && m < 60) ? m : 0;
        seconds = (s >= 0 && s < 60) ? s : 0;
    }

    // Add two time objects
    Time addTime(Time t) {
        Time result;
        result.seconds = seconds + t.seconds;
        result.minutes = minutes + t.minutes;
        result.hours = hours + t.hours;
        result.normalize();
        return result;
    }

    // Calculate difference in seconds
    int differenceInSeconds(Time t) {
        int thisTotal = hours * 3600 + minutes * 60 + seconds;
        int otherTotal = t.hours * 3600 + t.minutes * 60 + t.seconds;
        return abs(thisTotal - otherTotal);
    }

    // Convert time to total seconds
    int toSeconds() {
        return hours * 3600 + minutes * 60 + seconds;
    }

    // Display time in HH:MM:SS format
    void displayTime() {
        cout << setfill('0') << setw(2) << hours << ":"
             << setw(2) << minutes << ":"
             << setw(2) << seconds;
    }

    // Getters
    int getHours() { return hours; }
    int getMinutes() { return minutes; }
    int getSeconds() { return seconds; }
};

int main() {
    // Create time objects
    Time t1(10, 30, 45);
    Time t2(5, 45, 30);
    Time t3(14, 20, 15);
    Time t4(23, 50, 40);

    // Display all times
    cout << "========== TIME OBJECTS ==========" << endl;
    cout << "Time 1: ";
    t1.displayTime();
    cout << endl;
    
    cout << "Time 2: ";
    t2.displayTime();
    cout << endl;
    
    cout << "Time 3: ";
    t3.displayTime();
    cout << endl;
    
    cout << "Time 4: ";
    t4.displayTime();
    cout << endl;

    // Add times
    cout << "\n========== ADDING TIMES ==========" << endl;
    Time sum1 = t1.addTime(t2);
    cout << "Time 1 + Time 2 = ";
    sum1.displayTime();
    cout << endl;

    Time sum2 = t3.addTime(t4);
    cout << "Time 3 + Time 4 = ";
    sum2.displayTime();
    cout << " (wraps around 24 hours)" << endl;

    // Calculate differences
    cout << "\n========== TIME DIFFERENCES ==========" << endl;
    int diff1 = t1.differenceInSeconds(t2);
    cout << "Difference between Time 1 and Time 2: " 
         << diff1 << " seconds (" 
         << diff1 / 3600 << " hours, "
         << (diff1 % 3600) / 60 << " minutes, "
         << diff1 % 60 << " seconds)" << endl;

    int diff2 = t3.differenceInSeconds(t4);
    cout << "Difference between Time 3 and Time 4: " 
         << diff2 << " seconds" << endl;

    // Test overflow handling
    cout << "\n========== TESTING OVERFLOW ==========" << endl;
    Time t5(12, 45, 50);
    Time t6(8, 30, 25);
    
    cout << "Time 5: ";
    t5.displayTime();
    cout << endl;
    
    cout << "Time 6: ";
    t6.displayTime();
    cout << endl;
    
    Time sum3 = t5.addTime(t6);
    cout << "Sum (with overflow handling): ";
    sum3.displayTime();
    cout << endl;

    // Test validation
    cout << "\n========== TESTING VALIDATION ==========" << endl;
    Time invalid(25, 70, 80);  // Invalid values
    cout << "Created time with invalid values (25:70:80)" << endl;
    cout << "Actual time stored: ";
    invalid.displayTime();
    cout << " (invalid values set to 0)" << endl;

    return 0;
}
```

</details>