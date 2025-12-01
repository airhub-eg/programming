# Exercise 4: Student Grade System
Create a `Student` class with:
- Private members: name, rollNumber, marks in 3 subjects
- Constructor
- Method `calculateAverage()` to return average marks
- Method `getGrade()` to return grade (A, B, C, D, F based on average)
- Method `displayReport()` to show complete report card
- Create 5 students, calculate their grades, and find the student with highest average

**Solution:**
<details> <summary>Solution</summary>

```cpp
#include <iostream>
#include <string>
using namespace std;

class Student {
private:
    string name;
    int rollNumber;
    float marks1, marks2, marks3;

public:
    // Constructor
    Student(string n, int roll, float m1, float m2, float m3) {
        name = n;
        rollNumber = roll;
        marks1 = m1;
        marks2 = m2;
        marks3 = m3;
    }

    // Calculate average marks
    float calculateAverage() {
        return (marks1 + marks2 + marks3) / 3.0;
    }

    // Get grade based on average
    char getGrade() {
        float avg = calculateAverage();
        if (avg >= 90) return 'A';
        else if (avg >= 80) return 'B';
        else if (avg >= 70) return 'C';
        else if (avg >= 60) return 'D';
        else return 'F';
    }

    // Display complete report card
    void displayReport() {
        cout << "\n========== REPORT CARD ==========" << endl;
        cout << "Name: " << name << endl;
        cout << "Roll Number: " << rollNumber << endl;
        cout << "Subject 1 Marks: " << marks1 << endl;
        cout << "Subject 2 Marks: " << marks2 << endl;
        cout << "Subject 3 Marks: " << marks3 << endl;
        cout << "Average: " << calculateAverage() << endl;
        cout << "Grade: " << getGrade() << endl;
        cout << "=================================" << endl;
    }

    // Getter for name
    string getName() {
        return name;
    }
};

int main() {
    // Creating 5 students
    Student students[5] = {
        Student("Alice Johnson", 101, 85, 90, 88),
        Student("Bob Smith", 102, 78, 82, 75),
        Student("Charlie Brown", 103, 92, 95, 98),
        Student("Diana Prince", 104, 88, 84, 90),
        Student("Eve Davis", 105, 65, 70, 68)
    };

    // Display all student reports
    for (int i = 0; i < 5; i++) {
        students[i].displayReport();
    }

    // Find student with highest average
    int highestIndex = 0;
    float highestAvg = students[0].calculateAverage();

    for (int i = 1; i < 5; i++) {
        float currentAvg = students[i].calculateAverage();
        if (currentAvg > highestAvg) {
            highestAvg = currentAvg;
            highestIndex = i;
        }
    }

    cout << "\n***** TOPPER *****" << endl;
    cout << "Student with highest average: " << students[highestIndex].getName() << endl;
    cout << "Average marks: " << highestAvg << endl;

    return 0;
}
```

</details>