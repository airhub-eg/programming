# Exercise 12: Student Attendance System
Create a `Student` class with:
- Private members: name, rollNumber, totalClasses, attendedClasses
- Constructor
- Methods: `markPresent()`, `markAbsent()`, `getAttendancePercentage()`
- Method `isEligibleForExam()` (requires 75% attendance)
- Create a class of 20 students, mark random attendance for 30 days, display students with low attendance

**Solution:**
<details> <summary>Solution</summary>

```cpp
#include <iostream>
#include <string>
#include <cstdlib>
#include <ctime>
using namespace std;

class Student {
private:
    string name;
    int rollNumber;
    int totalClasses;
    int attendedClasses;

public:
    // Constructor
    Student(string n = "", int roll = 0) {
        name = n;
        rollNumber = roll;
        totalClasses = 0;
        attendedClasses = 0;
    }

    // Mark present
    void markPresent() {
        totalClasses++;
        attendedClasses++;
    }

    // Mark absent
    void markAbsent() {
        totalClasses++;
    }

    // Get attendance percentage
    double getAttendancePercentage() {
        if (totalClasses == 0) return 0.0;
        return (attendedClasses * 100.0) / totalClasses;
    }

    // Check eligibility for exam
    bool isEligibleForExam() {
        return getAttendancePercentage() >= 75.0;
    }

    // Display student info
    void displayInfo() {
        cout << "Roll: " << rollNumber << " | Name: " << name 
             << " | Attended: " << attendedClasses << "/" << totalClasses
             << " | Percentage: " << getAttendancePercentage() << "%"
             << " | Eligible: " << (isEligibleForExam() ? "Yes" : "No") << endl;
    }

    // Getters
    string getName() { return name; }
    int getRollNumber() { return rollNumber; }
    int getTotalClasses() { return totalClasses; }
    int getAttendedClasses() { return attendedClasses; }
};

int main() {
    srand(time(0));  // Seed random number generator

    const int NUM_STUDENTS = 20;
    const int NUM_DAYS = 30;

    // Create array of students
    Student students[NUM_STUDENTS] = {
        Student("Alice Johnson", 101),
        Student("Bob Smith", 102),
        Student("Charlie Brown", 103),
        Student("Diana Prince", 104),
        Student("Eve Davis", 105),
        Student("Frank Wilson", 106),
        Student("Grace Lee", 107),
        Student("Henry Taylor", 108),
        Student("Iris Martinez", 109),
        Student("Jack Anderson", 110),
        Student("Kelly Thomas", 111),
        Student("Liam Jackson", 112),
        Student("Mia White", 113),
        Student("Noah Harris", 114),
        Student("Olivia Martin", 115),
        Student("Peter Thompson", 116),
        Student("Quinn Garcia", 117),
        Student("Rachel Rodriguez", 118),
        Student("Samuel Lewis", 119),
        Student("Tara Walker", 120)
    };

    cout << "========== MARKING ATTENDANCE FOR " << NUM_DAYS << " DAYS ==========" << endl;

    // Mark attendance for 30 days
    for (int day = 1; day <= NUM_DAYS; day++) {
        cout << "\nDay " << day << ": ";
        int presentCount = 0;
        
        for (int i = 0; i < NUM_STUDENTS; i++) {
            // Random attendance (70% chance of being present)
            int random = rand() % 100;
            if (random < 70) {
                students[i].markPresent();
                presentCount++;
            } else {
                students[i].markAbsent();
            }
        }
        
        cout << presentCount << "/" << NUM_STUDENTS << " students present" << endl;
    }

    // Display all student attendance
    cout << "\n========== COMPLETE ATTENDANCE REPORT ==========" << endl;
    for (int i = 0; i < NUM_STUDENTS; i++) {
        students[i].displayInfo();
    }

    // Find and display students with low attendance
    cout << "\n========== STUDENTS WITH LOW ATTENDANCE (<75%) ==========" << endl;
    bool foundLowAttendance = false;
    for (int i = 0; i < NUM_STUDENTS; i++) {
        if (!students[i].isEligibleForExam()) {
            students[i].displayInfo();
            foundLowAttendance = true;
        }
    }
    
    if (!foundLowAttendance) {
        cout << "No students with low attendance. Great job!" << endl;
    }

    // Display statistics
    cout << "\n========== ATTENDANCE STATISTICS ==========" << endl;
    int eligible = 0;
    int notEligible = 0;
    double totalPercentage = 0;

    for (int i = 0; i < NUM_STUDENTS; i++) {
        if (students[i].isEligibleForExam()) {
            eligible++;
        } else {
            notEligible++;
        }
        totalPercentage += students[i].getAttendancePercentage();
    }

    double averageAttendance = totalPercentage / NUM_STUDENTS;

    cout << "Total Students: " << NUM_STUDENTS << endl;
    cout << "Eligible for Exam: " << eligible << " (" 
         << (eligible * 100.0 / NUM_STUDENTS) << "%)" << endl;
    cout << "Not Eligible: " << notEligible << " (" 
         << (notEligible * 100.0 / NUM_STUDENTS) << "%)" << endl;
    cout << "Average Class Attendance: " << averageAttendance << "%" << endl;

    // Find student with highest and lowest attendance
    int highestIndex = 0, lowestIndex = 0;
    for (int i = 1; i < NUM_STUDENTS; i++) {
        if (students[i].getAttendancePercentage() > students[highestIndex].getAttendancePercentage()) {
            highestIndex = i;
        }
        if (students[i].getAttendancePercentage() < students[lowestIndex].getAttendancePercentage()) {
            lowestIndex = i;
        }
    }

    cout << "\nHighest Attendance: " << students[highestIndex].getName() 
         << " (" << students[highestIndex].getAttendancePercentage() << "%)" << endl;
    cout << "Lowest Attendance: " << students[lowestIndex].getName() 
         << " (" << students[lowestIndex].getAttendancePercentage() << "%)" << endl;

    return 0;
}
```

</details>