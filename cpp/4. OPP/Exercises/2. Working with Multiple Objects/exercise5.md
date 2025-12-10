# Exercise 5: Employee Management
Create an `Employee` class with:
- Private members: empID, name, salary, department
- Constructor
- Method `applyRaise(percentage)` to increase salary
- Method `changeDepartment(newDept)`
- Method `displayDetails()`
- Create an array of 5 employees, give a 10% raise to all employees in "Sales" department

**Solution:**
<details> <summary>Solution</summary>

```cpp
#include <iostream>
#include <string>
using namespace std;

class Employee {
private:
    int empID;
    string name;
    double salary;
    string department;

public:
    // Constructor
    Employee(int id, string n, double sal, string dept) {
        empID = id;
        name = n;
        salary = sal;
        department = dept;
    }

    // Apply raise to salary
    void applyRaise(double percentage) {
        double raiseAmount = salary * (percentage / 100.0);
        salary += raiseAmount;
        cout << name << " received a " << percentage << "% raise of $" 
             << raiseAmount << endl;
    }

    // Change department
    void changeDepartment(string newDept) {
        cout << name << " moved from " << department << " to " << newDept << endl;
        department = newDept;
    }

    // Display employee details
    void displayDetails() {
        cout << "\n--- Employee Details ---" << endl;
        cout << "ID: " << empID << endl;
        cout << "Name: " << name << endl;
        cout << "Salary: $" << salary << endl;
        cout << "Department: " << department << endl;
    }

    // Getter for department
    string getDepartment() {
        return department;
    }

    // Getter for name
    string getName() {
        return name;
    }
};

int main() {
    // Creating array of 5 employees
    Employee employees[5] = {
        Employee(101, "John Doe", 50000, "Sales"),
        Employee(102, "Jane Smith", 60000, "Engineering"),
        Employee(103, "Mike Johnson", 45000, "Sales"),
        Employee(104, "Sarah Williams", 55000, "Marketing"),
        Employee(105, "Tom Brown", 48000, "Sales")
    };

    // Display all employees before raise
    cout << "========== INITIAL EMPLOYEE DATA ==========" << endl;
    for (int i = 0; i < 5; i++) {
        employees[i].displayDetails();
    }

    // Give 10% raise to all employees in Sales department
    cout << "\n========== APPLYING 10% RAISE TO SALES DEPT ==========" << endl;
    for (int i = 0; i < 5; i++) {
        if (employees[i].getDepartment() == "Sales") {
            employees[i].applyRaise(10.0);
        }
    }

    // Display all employees after raise
    cout << "\n========== UPDATED EMPLOYEE DATA ==========" << endl;
    for (int i = 0; i < 5; i++) {
        employees[i].displayDetails();
    }

    // Test department change
    cout << "\n========== DEPARTMENT CHANGE ==========" << endl;
    employees[1].changeDepartment("Research & Development");
    employees[1].displayDetails();

    return 0;
}
```

</details>