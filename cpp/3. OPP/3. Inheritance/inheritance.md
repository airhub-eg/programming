# Inheritance in C++

## What is Inheritance?

**Inheritance** is a fundamental concept in Object-Oriented Programming (OOP) that allows a class to acquire properties (data members) and behaviors (member functions) from another class. It establishes an "IS-A" relationship between classes.

**Real-World Analogy:**
- A **Car** is a type of **Vehicle**
- A **Dog** is a type of **Animal**
- A **Student** is a type of **Person**

In these examples, Car, Dog, and Student inherit common characteristics from Vehicle, Animal, and Person respectively, while also having their own unique features.

## Key Terminology

- **Base Class (Parent/Super Class)**: The class whose properties are inherited
- **Derived Class (Child/Sub Class)**: The class that inherits from the base class
- **Inheritance**: The mechanism of deriving a new class from an existing class

## Why Use Inheritance?

1. **Code Reusability**: Reuse existing code without rewriting it
2. **Extensibility**: Add new features to existing classes
3. **Maintainability**: Changes in base class automatically reflect in derived classes
4. **Hierarchical Classification**: Organize classes in a logical hierarchy
5. **Polymorphism**: Foundation for runtime polymorphism

## Basic Syntax

```cpp
class BaseClass {
    // Base class members
};

class DerivedClass : access_specifier BaseClass {
    // Derived class members
};
```

## Types of Inheritance

### 1. Single Inheritance

One derived class inherits from one base class.

```
    Base
     |
  Derived
```

### 2. Multiple Inheritance

One derived class inherits from multiple base classes.

```
  Base1    Base2
     \      /
      Derived
```

### 3. Multilevel Inheritance

A derived class inherits from another derived class (chain of inheritance).

```
    Base
     |
  Derived1
     |
  Derived2
```

### 4. Hierarchical Inheritance

Multiple derived classes inherit from one base class.

```
      Base
    /  |  \
   D1  D2  D3
```

### 5. Hybrid Inheritance

Combination of two or more types of inheritance.

```
      Base
     /    \
   D1      D2
     \    /
       D3
```

## Access Specifiers in Inheritance

Access specifiers control how base class members are accessible in derived class:

| Base Class Member | Public Inheritance | Protected Inheritance | Private Inheritance |
|-------------------|-------------------|----------------------|---------------------|
| Public | Public | Protected | Private |
| Protected | Protected | Protected | Private |
| Private | Not Accessible | Not Accessible | Not Accessible |

**Key Points:**
- **Private members** of base class are NEVER directly accessible in derived class
- **Public inheritance**: IS-A relationship (most common)
- **Protected inheritance**: Rarely used
- **Private inheritance**: HAS-A relationship (composition alternative)

##  Examples

**Example 1:**
<details> <summary>Show</summary>

```cpp
#include <iostream>
#include <string>
using namespace std;

// ========== EXAMPLE 1: SINGLE INHERITANCE ==========

class Person {
protected:
    string name;
    int age;
    
public:
    Person() {
        name = "Unknown";
        age = 0;
        cout << "Person default constructor called" << endl;
    }
    
    Person(string n, int a) {
        name = n;
        age = a;
        cout << "Person parameterized constructor called for " << name << endl;
    }
    
    void displayPerson() {
        cout << "Name: " << name << endl;
        cout << "Age: " << age << endl;
    }
    
    void eat() {
        cout << name << " is eating." << endl;
    }
    
    void sleep() {
        cout << name << " is sleeping." << endl;
    }
};

// Student inherits from Person
class Student : public Person {
private:
    int rollNumber;
    float gpa;
    
public:
    Student() : Person() {
        rollNumber = 0;
        gpa = 0.0;
        cout << "Student default constructor called" << endl;
    }
    
    Student(string n, int a, int roll, float g) : Person(n, a) {
        rollNumber = roll;
        gpa = g;
        cout << "Student parameterized constructor called" << endl;
    }
    
    void study() {
        cout << name << " is studying." << endl;
    }
    
    void displayStudent() {
        displayPerson();  // Calling base class method
        cout << "Roll Number: " << rollNumber << endl;
        cout << "GPA: " << gpa << endl;
    }
};

// ========== EXAMPLE 2: MULTILEVEL INHERITANCE ==========

class Vehicle {
protected:
    string brand;
    int year;
    
public:
    Vehicle(string b, int y) {
        brand = b;
        year = y;
        cout << "Vehicle constructor called" << endl;
    }
    
    void displayVehicle() {
        cout << "Brand: " << brand << endl;
        cout << "Year: " << year << endl;
    }
    
    void honk() {
        cout << "Vehicle is honking!" << endl;
    }
};

class Car : public Vehicle {
protected:
    int doors;
    
public:
    Car(string b, int y, int d) : Vehicle(b, y) {
        doors = d;
        cout << "Car constructor called" << endl;
    }
    
    void displayCar() {
        displayVehicle();
        cout << "Doors: " << doors << endl;
    }
    
    void drive() {
        cout << brand << " car is driving." << endl;
    }
};

class SportsCar : public Car {
private:
    int topSpeed;
    
public:
    SportsCar(string b, int y, int d, int speed) : Car(b, y, d) {
        topSpeed = speed;
        cout << "SportsCar constructor called" << endl;
    }
    
    void displaySportsCar() {
        displayCar();
        cout << "Top Speed: " << topSpeed << " km/h" << endl;
    }
    
    void turboBoost() {
        cout << brand << " sports car activated turbo boost!" << endl;
    }
};

// ========== EXAMPLE 3: HIERARCHICAL INHERITANCE ==========

class Shape {
protected:
    string color;
    
public:
    Shape(string c) {
        color = c;
        cout << "Shape constructor called" << endl;
    }
    
    void displayColor() {
        cout << "Color: " << color << endl;
    }
};

class Circle : public Shape {
private:
    double radius;
    
public:
    Circle(string c, double r) : Shape(c) {
        radius = r;
        cout << "Circle constructor called" << endl;
    }
    
    double area() {
        return 3.14159 * radius * radius;
    }
    
    void display() {
        cout << "\n--- Circle ---" << endl;
        displayColor();
        cout << "Radius: " << radius << endl;
        cout << "Area: " << area() << endl;
    }
};

class Rectangle : public Shape {
private:
    double length;
    double width;
    
public:
    Rectangle(string c, double l, double w) : Shape(c) {
        length = l;
        width = w;
        cout << "Rectangle constructor called" << endl;
    }
    
    double area() {
        return length * width;
    }
    
    void display() {
        cout << "\n--- Rectangle ---" << endl;
        displayColor();
        cout << "Length: " << length << endl;
        cout << "Width: " << width << endl;
        cout << "Area: " << area() << endl;
    }
};

class Triangle : public Shape {
private:
    double base;
    double height;
    
public:
    Triangle(string c, double b, double h) : Shape(c) {
        base = b;
        height = h;
        cout << "Triangle constructor called" << endl;
    }
    
    double area() {
        return 0.5 * base * height;
    }
    
    void display() {
        cout << "\n--- Triangle ---" << endl;
        displayColor();
        cout << "Base: " << base << endl;
        cout << "Height: " << height << endl;
        cout << "Area: " << area() << endl;
    }
};

// ========== MAIN FUNCTION ==========

int main() {
    cout << "========== SINGLE INHERITANCE EXAMPLE ==========" << endl;
    Student s1("Alice Johnson", 20, 101, 3.8);
    cout << "\nStudent Details:" << endl;
    s1.displayStudent();
    cout << "\nStudent Activities:" << endl;
    s1.eat();      // Inherited from Person
    s1.sleep();    // Inherited from Person
    s1.study();    // Student's own method
    
    cout << "\n\n========== MULTILEVEL INHERITANCE EXAMPLE ==========" << endl;
    SportsCar sc("Ferrari", 2024, 2, 350);
    cout << "\nSports Car Details:" << endl;
    sc.displaySportsCar();
    cout << "\nSports Car Actions:" << endl;
    sc.honk();        // Inherited from Vehicle
    sc.drive();       // Inherited from Car
    sc.turboBoost();  // SportsCar's own method
    
    cout << "\n\n========== HIERARCHICAL INHERITANCE EXAMPLE ==========" << endl;
    Circle c("Red", 5.0);
    Rectangle r("Blue", 4.0, 6.0);
    Triangle t("Green", 3.0, 8.0);
    
    c.display();
    r.display();
    t.display();
    
    return 0;
}
```

</details>

**Example 2:**
<details> <summary>Show</summary>

```cpp
#include <iostream>
#include <string>
using namespace std;

// ========== EXAMPLE 4: MULTIPLE INHERITANCE ==========

class Engine {
protected:
    string engineType;
    int horsepower;
    
public:
    Engine(string type, int hp) {
        engineType = type;
        horsepower = hp;
        cout << "Engine constructor called" << endl;
    }
    
    void displayEngine() {
        cout << "Engine Type: " << engineType << endl;
        cout << "Horsepower: " << horsepower << endl;
    }
    
    void start() {
        cout << "Engine started: " << engineType << endl;
    }
};

class Body {
protected:
    string bodyType;
    string color;
    
public:
    Body(string type, string c) {
        bodyType = type;
        color = c;
        cout << "Body constructor called" << endl;
    }
    
    void displayBody() {
        cout << "Body Type: " << bodyType << endl;
        cout << "Color: " << color << endl;
    }
    
    void paint(string newColor) {
        color = newColor;
        cout << "Body repainted to " << newColor << endl;
    }
};

// Multiple Inheritance: Automobile inherits from both Engine and Body
class Automobile : public Engine, public Body {
private:
    string model;
    int year;
    
public:
    Automobile(string m, int y, string eType, int hp, string bType, string c) 
        : Engine(eType, hp), Body(bType, c) {
        model = m;
        year = y;
        cout << "Automobile constructor called" << endl;
    }
    
    void displayAutomobile() {
        cout << "\n=== Automobile Details ===" << endl;
        cout << "Model: " << model << endl;
        cout << "Year: " << year << endl;
        displayEngine();
        displayBody();
    }
};

// ========== EXAMPLE 5: ACCESS SPECIFIERS IN INHERITANCE ==========

class Base {
private:
    int privateData;
    
protected:
    int protectedData;
    
public:
    int publicData;
    
    Base() {
        privateData = 10;
        protectedData = 20;
        publicData = 30;
    }
    
    void showBase() {
        cout << "Private Data: " << privateData << endl;
        cout << "Protected Data: " << protectedData << endl;
        cout << "Public Data: " << publicData << endl;
    }
};

// Public Inheritance
class PublicDerived : public Base {
public:
    void accessMembers() {
        cout << "\n--- Public Inheritance ---" << endl;
        // privateData = 100;  // ERROR: Cannot access private member
        protectedData = 200;   // OK: Protected becomes protected
        publicData = 300;      // OK: Public remains public
        cout << "Protected Data: " << protectedData << endl;
        cout << "Public Data: " << publicData << endl;
    }
};

// Protected Inheritance
class ProtectedDerived : protected Base {
public:
    void accessMembers() {
        cout << "\n--- Protected Inheritance ---" << endl;
        // privateData = 100;  // ERROR: Cannot access private member
        protectedData = 400;   // OK: Protected becomes protected
        publicData = 500;      // OK: Public becomes protected
        cout << "Protected Data: " << protectedData << endl;
        cout << "Public Data: " << publicData << endl;
    }
};

// Private Inheritance
class PrivateDerived : private Base {
public:
    void accessMembers() {
        cout << "\n--- Private Inheritance ---" << endl;
        // privateData = 100;  // ERROR: Cannot access private member
        protectedData = 600;   // OK: Protected becomes private
        publicData = 700;      // OK: Public becomes private
        cout << "Protected Data: " << protectedData << endl;
        cout << "Public Data: " << publicData << endl;
    }
};

// ========== EXAMPLE 6: FUNCTION OVERRIDING ==========

class Animal {
protected:
    string name;
    
public:
    Animal(string n) {
        name = n;
    }
    
    void eat() {
        cout << name << " is eating." << endl;
    }
    
    // Virtual function for overriding
    virtual void makeSound() {
        cout << name << " makes a sound." << endl;
    }
    
    void sleep() {
        cout << name << " is sleeping." << endl;
    }
};

class Dog : public Animal {
private:
    string breed;
    
public:
    Dog(string n, string b) : Animal(n) {
        breed = b;
    }
    
    // Overriding makeSound()
    void makeSound() override {
        cout << name << " barks: Woof! Woof!" << endl;
    }
    
    void fetch() {
        cout << name << " is fetching the ball." << endl;
    }
};

class Cat : public Animal {
private:
    bool isIndoor;
    
public:
    Cat(string n, bool indoor) : Animal(n) {
        isIndoor = indoor;
    }
    
    // Overriding makeSound()
    void makeSound() override {
        cout << name << " meows: Meow! Meow!" << endl;
    }
    
    void climb() {
        cout << name << " is climbing." << endl;
    }
};

// ========== EXAMPLE 7: CONSTRUCTOR AND DESTRUCTOR CHAIN ==========

class GrandParent {
public:
    GrandParent() {
        cout << "1. GrandParent constructor" << endl;
    }
    
    ~GrandParent() {
        cout << "6. GrandParent destructor" << endl;
    }
};

class Parent : public GrandParent {
public:
    Parent() {
        cout << "2. Parent constructor" << endl;
    }
    
    ~Parent() {
        cout << "5. Parent destructor" << endl;
    }
};

class Child : public Parent {
public:
    Child() {
        cout << "3. Child constructor" << endl;
    }
    
    ~Child() {
        cout << "4. Child destructor" << endl;
    }
};

// ========== EXAMPLE 8: HYBRID INHERITANCE ==========

class Device {
protected:
    string brand;
    
public:
    Device(string b) {
        brand = b;
        cout << "Device constructor" << endl;
    }
    
    void displayBrand() {
        cout << "Brand: " << brand << endl;
    }
};

class Phone : virtual public Device {
protected:
    string phoneNumber;
    
public:
    Phone(string b, string num) : Device(b) {
        phoneNumber = num;
        cout << "Phone constructor" << endl;
    }
    
    void call() {
        cout << "Making a call from " << phoneNumber << endl;
    }
};

class Camera : virtual public Device {
protected:
    int megapixels;
    
public:
    Camera(string b, int mp) : Device(b) {
        megapixels = mp;
        cout << "Camera constructor" << endl;
    }
    
    void takePhoto() {
        cout << "Taking photo with " << megapixels << "MP camera" << endl;
    }
};

class SmartPhone : public Phone, public Camera {
private:
    string os;
    
public:
    SmartPhone(string b, string num, int mp, string operating) 
        : Device(b), Phone(b, num), Camera(b, mp) {
        os = operating;
        cout << "SmartPhone constructor" << endl;
    }
    
    void displaySmartPhone() {
        cout << "\n=== SmartPhone Details ===" << endl;
        displayBrand();  // No ambiguity due to virtual inheritance
        cout << "Phone Number: " << phoneNumber << endl;
        cout << "Camera: " << megapixels << "MP" << endl;
        cout << "Operating System: " << os << endl;
    }
};

// ========== MAIN FUNCTION ==========

int main() {
    cout << "========== MULTIPLE INHERITANCE EXAMPLE ==========" << endl;
    Automobile car("Tesla Model S", 2024, "Electric", 670, "Sedan", "Red");
    car.displayAutomobile();
    car.start();
    car.paint("Blue");
    
    cout << "\n\n========== ACCESS SPECIFIERS EXAMPLE ==========" << endl;
    PublicDerived pd;
    pd.accessMembers();
    pd.publicData = 999;  // Accessible because public inheritance
    
    ProtectedDerived ptd;
    ptd.accessMembers();
    // ptd.publicData = 999;  // ERROR: Not accessible (became protected)
    
    PrivateDerived pvd;
    pvd.accessMembers();
    // pvd.publicData = 999;  // ERROR: Not accessible (became private)
    
    cout << "\n\n========== FUNCTION OVERRIDING EXAMPLE ==========" << endl;
    Dog dog("Buddy", "Golden Retriever");
    Cat cat("Whiskers", true);
    
    dog.makeSound();  // Calls Dog's overridden version
    dog.eat();        // Inherited from Animal
    dog.fetch();      // Dog's own method
    
    cout << endl;
    
    cat.makeSound();  // Calls Cat's overridden version
    cat.eat();        // Inherited from Animal
    cat.climb();      // Cat's own method
    
    cout << "\n\n========== CONSTRUCTOR/DESTRUCTOR CHAIN ==========" << endl;
    {
        Child c;
        cout << "Child object exists here" << endl;
    }  // Destructors called automatically
    
    cout << "\n\n========== HYBRID INHERITANCE (DIAMOND PROBLEM) ==========" << endl;
    SmartPhone sp("Apple", "+1-555-1234", 48, "iOS");
    sp.displaySmartPhone();
    sp.call();
    sp.takePhoto();
    
    return 0;
}
```

</details>

**Example 3:**
<details> <summary>Show</summary>

```cpp
#include <iostream>
#include <string>
using namespace std;

// ========== BASE CLASS: EMPLOYEE ==========

class Employee {
protected:
    int empID;
    string name;
    string department;
    double baseSalary;
    
public:
    Employee(int id, string n, string dept, double salary) {
        empID = id;
        name = n;
        department = dept;
        baseSalary = salary;
        cout << "Employee " << name << " created" << endl;
    }
    
    virtual ~Employee() {
        cout << "Employee " << name << " removed" << endl;
    }
    
    // Virtual function for salary calculation
    virtual double calculateSalary() {
        return baseSalary;
    }
    
    // Virtual function for displaying info
    virtual void displayInfo() {
        cout << "\n=== Employee Information ===" << endl;
        cout << "ID: " << empID << endl;
        cout << "Name: " << name << endl;
        cout << "Department: " << department << endl;
        cout << "Base Salary: $" << baseSalary << endl;
    }
    
    void work() {
        cout << name << " is working." << endl;
    }
    
    // Getters
    string getName() { return name; }
    int getID() { return empID; }
};

// ========== DERIVED CLASS: MANAGER ==========

class Manager : public Employee {
private:
    int teamSize;
    double bonus;
    
public:
    Manager(int id, string n, string dept, double salary, int team, double b) 
        : Employee(id, n, dept, salary) {
        teamSize = team;
        bonus = b;
        cout << "Manager role assigned" << endl;
    }
    
    // Override salary calculation
    double calculateSalary() override {
        return baseSalary + bonus + (teamSize * 500);  // $500 per team member
    }
    
    // Override display info
    void displayInfo() override {
        Employee::displayInfo();  // Call base class method
        cout << "Position: Manager" << endl;
        cout << "Team Size: " << teamSize << endl;
        cout << "Performance Bonus: $" << bonus << endl;
        cout << "Total Salary: $" << calculateSalary() << endl;
    }
    
    void conductMeeting() {
        cout << name << " is conducting a team meeting with " 
             << teamSize << " members." << endl;
    }
    
    void evaluateTeam() {
        cout << name << " is evaluating team performance." << endl;
    }
};

// ========== DERIVED CLASS: DEVELOPER ==========

class Developer : public Employee {
private:
    string programmingLanguage;
    int projectsCompleted;
    
public:
    Developer(int id, string n, string dept, double salary, string lang, int projects) 
        : Employee(id, n, dept, salary) {
        programmingLanguage = lang;
        projectsCompleted = projects;
        cout << "Developer role assigned" << endl;
    }
    
    // Override salary calculation
    double calculateSalary() override {
        return baseSalary + (projectsCompleted * 1000);  // $1000 per project
    }
    
    // Override display info
    void displayInfo() override {
        Employee::displayInfo();
        cout << "Position: Developer" << endl;
        cout << "Primary Language: " << programmingLanguage << endl;
        cout << "Projects Completed: " << projectsCompleted << endl;
        cout << "Total Salary: $" << calculateSalary() << endl;
    }
    
    void writeCode() {
        cout << name << " is writing " << programmingLanguage << " code." << endl;
    }
    
    void debugCode() {
        cout << name << " is debugging code." << endl;
    }
};

// ========== DERIVED CLASS: SALESPERSON ==========

class Salesperson : public Employee {
private:
    double salesTarget;
    double salesAchieved;
    double commissionRate;
    
public:
    Salesperson(int id, string n, string dept, double salary, 
                double target, double achieved, double rate) 
        : Employee(id, n, dept, salary) {
        salesTarget = target;
        salesAchieved = achieved;
        commissionRate = rate;
        cout << "Salesperson role assigned" << endl;
    }
    
    // Override salary calculation
    double calculateSalary() override {
        double commission = salesAchieved * (commissionRate / 100.0);
        return baseSalary + commission;
    }
    
    // Override display info
    void displayInfo() override {
        Employee::displayInfo();
        cout << "Position: Salesperson" << endl;
        cout << "Sales Target: $" << salesTarget << endl;
        cout << "Sales Achieved: $" << salesAchieved << endl;
        cout << "Commission Rate: " << commissionRate << "%" << endl;
        cout << "Commission Earned: $" << (salesAchieved * commissionRate / 100.0) << endl;
        cout << "Total Salary: $" << calculateSalary() << endl;
    }
    
    void makeSale(double amount) {
        salesAchieved += amount;
        cout << name << " made a sale of $" << amount << endl;
        cout << "Total sales: $" << salesAchieved << endl;
    }
    
    void meetClient() {
        cout << name << " is meeting with a client." << endl;
    }
};

// ========== DERIVED CLASS: INTERN ==========

class Intern : public Employee {
private:
    string university;
    int internshipMonths;
    
public:
    Intern(int id, string n, string dept, double salary, string uni, int months) 
        : Employee(id, n, dept, salary) {
        university = uni;
        internshipMonths = months;
        cout << "Intern role assigned" << endl;
    }
    
    // Override salary calculation (fixed stipend)
    double calculateSalary() override {
        return baseSalary;  // No bonus for interns
    }
    
    // Override display info
    void displayInfo() override {
        Employee::displayInfo();
        cout << "Position: Intern" << endl;
        cout << "University: " << university << endl;
        cout << "Internship Duration: " << internshipMonths << " months" << endl;
        cout << "Monthly Stipend: $" << calculateSalary() << endl;
    }
    
    void learn() {
        cout << name << " is learning new skills." << endl;
    }
    
    void attendTraining() {
        cout << name << " is attending training session." << endl;
    }
};

// ========== COMPANY CLASS (MANAGES EMPLOYEES) ==========

class Company {
private:
    string companyName;
    Employee* employees[10];
    int employeeCount;
    
public:
    Company(string name) {
        companyName = name;
        employeeCount = 0;
        cout << "\n" << companyName << " established!" << endl;
    }
    
    void hireEmployee(Employee* emp) {
        if (employeeCount < 10) {
            employees[employeeCount] = emp;
            employeeCount++;
            cout << emp->getName() << " hired!" << endl;
        } else {
            cout << "Company is at full capacity!" << endl;
        }
    }
    
    void displayAllEmployees() {
        cout << "\n========================================" << endl;
        cout << "     " << companyName << " - Employee Roster" << endl;
        cout << "========================================" << endl;
        
        for (int i = 0; i < employeeCount; i++) {
            employees[i]->displayInfo();
        }
    }
    
    void calculateTotalPayroll() {
        double total = 0;
        cout << "\n========================================" << endl;
        cout << "          Payroll Calculation" << endl;
        cout << "========================================" << endl;
        
        for (int i = 0; i < employeeCount; i++) {
            double salary = employees[i]->calculateSalary();
            total += salary;
            cout << employees[i]->getName() << ": $" << salary << endl;
        }
        
        cout << "----------------------------------------" << endl;
        cout << "Total Payroll: $" << total << endl;
        cout << "========================================" << endl;
    }
};

// ========== MAIN FUNCTION ==========

int main() {
    cout << "========== EMPLOYEE MANAGEMENT SYSTEM ==========" << endl;
    
    // Create company
    Company techCorp("TechCorp Solutions");
    
    cout << "\n========== HIRING EMPLOYEES ==========" << endl;
    
    // Create different types of employees
    Manager m1(101, "Sarah Johnson", "Engineering", 80000, 8, 15000);
    Developer d1(102, "Mike Chen", "Engineering", 70000, "C++", 12);
    Developer d2(103, "Emily Davis", "Engineering", 65000, "Python", 8);
    Salesperson s1(104, "Robert Brown", "Sales", 50000, 100000, 85000, 5);
    Salesperson s2(105, "Lisa Anderson", "Sales", 50000, 120000, 95000, 5);
    Intern i1(106, "Tom Wilson", "Engineering", 2000, "MIT", 6);
    
    // Hire employees
    techCorp.hireEmployee(&m1);
    techCorp.hireEmployee(&d1);
    techCorp.hireEmployee(&d2);
    techCorp.hireEmployee(&s1);
    techCorp.hireEmployee(&s2);
    techCorp.hireEmployee(&i1);
    
    // Display all employees
    techCorp.displayAllEmployees();
    
    // Calculate total payroll
    techCorp.calculateTotalPayroll();
    
    // Demonstrate specific behaviors
    cout << "\n========== DAILY ACTIVITIES ==========" << endl;
    m1.conductMeeting();
    m1.evaluateTeam();
    
    d1.writeCode();
    d1.debugCode();
    
    s1.meetClient();
    s1.makeSale(12000);
    
    i1.learn();
    i1.attendTraining();
    
    // Demonstrate polymorphism
    cout << "\n========== POLYMORPHISM DEMONSTRATION ==========" << endl;
    Employee* empPtr;
    
    empPtr = &m1;
    cout << "\nPointing to Manager:" << endl;
    empPtr->work();
    cout << "Calculated Salary: $" << empPtr->calculateSalary() << endl;
    
    empPtr = &d1;
    cout << "\nPointing to Developer:" << endl;
    empPtr->work();
    cout << "Calculated Salary: $" << empPtr->calculateSalary() << endl;
    
    empPtr = &s1;
    cout << "\nPointing to Salesperson:" << endl;
    empPtr->work();
    cout << "Calculated Salary: $" << empPtr->calculateSalary() << endl;
    
    cout << "\n========== PROGRAM END ==========" << endl;
    
    return 0;
}
```
</details>

## Important Inheritance Concepts

### 1. Constructor Execution Order

When creating a derived class object:
1. **Base class constructor** executes first
2. **Derived class constructor** executes second

When destroying a derived class object:
1. **Derived class destructor** executes first
2. **Base class destructor** executes second

```cpp
class Base {
public:
    Base() { cout << "Base constructor" << endl; }
    ~Base() { cout << "Base destructor" << endl; }
};

class Derived : public Base {
public:
    Derived() { cout << "Derived constructor" << endl; }
    ~Derived() { cout << "Derived destructor" << endl; }
};

// Creating object:
// Output: Base constructor
//         Derived constructor

// Destroying object:
// Output: Derived destructor
//         Base destructor
```

### 2. Function Overriding vs Function Overloading

**Function Overriding** (Inheritance):
- Same function name in base and derived class
- Same signature (parameters)
- Different implementation
- Uses `virtual` keyword for runtime polymorphism

**Function Overloading** (Same class):
- Same function name
- Different parameters
- Different signature

```cpp
class Base {
public:
    virtual void display() {
        cout << "Base display" << endl;
    }
};

class Derived : public Base {
public:
    void display() override {  // Overriding
        cout << "Derived display" << endl;
    }
    
    void display(int x) {  // Overloading
        cout << "Derived display: " << x << endl;
    }
};
```

### 3. The Diamond Problem

Occurs in **multiple inheritance** when a class inherits from two classes that have a common base class.

```
      Base
      /  \
     D1   D2
      \  /
      Final
```

**Problem**: Final has two copies of Base class members (ambiguity).

**Solution**: Use **virtual inheritance**

```cpp
class Base {
public:
    int value;
};

class D1 : virtual public Base {
    // ...
};

class D2 : virtual public Base {
    // ...
};

class Final : public D1, public D2 {
    // Now only one copy of Base exists
};
```

### 4. Virtual Functions and Polymorphism

**Virtual functions** enable **runtime polymorphism** (late binding).

```cpp
class Animal {
public:
    virtual void makeSound() {
        cout << "Animal sound" << endl;
    }
};

class Dog : public Animal {
public:
    void makeSound() override {
        cout << "Woof!" << endl;
    }
};

// Polymorphism in action
Animal* ptr = new Dog();
ptr->makeSound();  // Outputs: Woof! (not "Animal sound")
```

**Key Points:**
- Use `virtual` in base class
- Use `override` in derived class (C++11+)
- Enables dynamic dispatch
- Slight performance overhead
- Essential for polymorphism

### 5. Abstract Classes and Pure Virtual Functions

An **abstract class** contains at least one **pure virtual function** and cannot be instantiated.

```cpp
class Shape {  // Abstract class
public:
    virtual double area() = 0;  // Pure virtual function
    virtual void display() = 0;
};

class Circle : public Shape {
private:
    double radius;
public:
    Circle(double r) : radius(r) {}
    
    double area() override {
        return 3.14159 * radius * radius;
    }
    
    void display() override {
        cout << "Circle with area: " << area() << endl;
    }
};

// Shape s;  // ERROR: Cannot instantiate abstract class
Circle c(5.0);  // OK
```

## When to Use Inheritance

### Good Uses of Inheritance:

1. **True IS-A Relationship**: Dog IS-A Animal
2. **Code Reusability**: Common functionality in base class
3. **Polymorphic Behavior**: Different objects responding differently
4. **Extending Existing Classes**: Adding features without modifying original

### When NOT to Use Inheritance:

1. **HAS-A Relationship**: Use composition instead
   - Car HAS-A Engine (composition, not inheritance)
2. **Just for Code Reuse**: Consider composition or utility classes
3. **Tight Coupling**: If changes in base affect all derived classes badly
4. **Deep Hierarchies**: More than 3-4 levels becomes hard to maintain

## Inheritance vs Composition

**Inheritance**: "IS-A" relationship
```cpp
class Dog : public Animal {
    // Dog IS-A Animal
};
```

**Composition**: "HAS-A" relationship
```cpp
class Car {
private:
    Engine engine;  // Car HAS-A Engine
    Wheels wheels;  // Car HAS-A Wheels
};
```

**When to choose:**
- Use **inheritance** for specialization (Dog is a specialized Animal)
- Use **composition** for building complex objects from parts (Car has parts)

## Common Inheritance Mistakes

### 1. Not Making Destructor Virtual

```cpp
class Base {
public:
    ~Base() {  // Should be virtual!
        // cleanup
    }
};

class Derived : public Base {
private:
    int* data;
public:
    ~Derived() {
        delete[] data;  // May not be called!
    }
};

Base* ptr = new Derived();
delete ptr;  // Only Base destructor called - memory leak!
```

**Fix**: Always make base class destructor virtual

```cpp
class Base {
public:
    virtual ~Base() {
        // cleanup
    }
};
```

### 2. Slicing Problem

```cpp
class Base {
public:
    int x;
};

class Derived : public Base {
public:
    int y;
};

Derived d;
d.x = 10;
d.y = 20;

Base b = d;  // SLICING: y is lost!
cout << b.x;  // 10
// b.y doesn't exist
```

**Fix**: Use pointers or references

```cpp
Base* ptr = &d;  // No slicing
Base& ref = d;   // No slicing
```

### 3. Calling Virtual Functions in Constructor

```cpp
class Base {
public:
    Base() {
        initialize();  // Calls Base::initialize, not Derived!
    }
    virtual void initialize() {
        cout << "Base init" << endl;
    }
};

class Derived : public Base {
public:
    void initialize() override {
        cout << "Derived init" << endl;
    }
};

Derived d;  // Outputs: "Base init" (not "Derived init")
```

## Summary for Inheritance

1. **Keep inheritance hierarchies shallow** (2-3 levels max)
2. **Make base class destructors virtual**
3. **Use `override` keyword** for clarity (C++11+)
4. **Prefer composition over inheritance** when possible
5. **Follow Liskov Substitution Principle**: Derived class should be substitutable for base class
6. **Make member functions virtual only when needed**
7. **Use protected for members needed by derived classes**
8. **Document inheritance relationships clearly**
9. **Avoid multiple inheritance unless necessary**
10. **Use abstract classes to define interfaces**
