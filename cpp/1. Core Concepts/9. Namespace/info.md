# Namespaces in C++

## Introduction to Namespaces
Namespaces are declarative regions that provide scope to identifiers (names of types, functions, variables, etc.) inside them. They are used to organize code into logical groups and to prevent name collisions.

## 1. Basic Namespace Usage

### Defining and Using Namespaces
```cpp
#include <iostream>
using namespace std;

// Define a namespace
namespace MathOperations {
    const double PI = 3.14159;
    
    double add(double a, double b) {
        return a + b;
    }
    
    double multiply(double a, double b) {
        return a * b;
    }
    
    double circleArea(double radius) {
        return PI * radius * radius;
    }
}

// Another namespace
namespace StringOperations {
    string concatenate(string a, string b) {
        return a + b;
    }
    
    int stringLength(string str) {
        return str.length();
    }
}

int main() {
    // Using namespace members with scope resolution operator
    cout << "PI = " << MathOperations::PI << endl;
    cout << "5 + 3 = " << MathOperations::add(5, 3) << endl;
    cout << "Circle area (r=5): " << MathOperations::circleArea(5) << endl;
    
    cout << "Concatenated: " << StringOperations::concatenate("Hello", " World") << endl;
    
    return 0;
}
```

## 2. `using` Directive and Declaration

### `using namespace` Directive
```cpp
#include <iostream>
using namespace std;

namespace Geometry {
    const double PI = 3.14159;
    
    class Circle {
    private:
        double radius;
    public:
        Circle(double r) : radius(r) {}
        
        double area() {
            return PI * radius * radius;
        }
        
        double circumference() {
            return 2 * PI * radius;
        }
    };
    
    class Rectangle {
    private:
        double length, width;
    public:
        Rectangle(double l, double w) : length(l), width(w) {}
        
        double area() {
            return length * width;
        }
        
        double perimeter() {
            return 2 * (length + width);
        }
    };
}

int main() {
    // Using the entire namespace
    using namespace Geometry;
    
    Circle circle(5.0);
    Rectangle rect(4.0, 6.0);
    
    cout << "Circle area: " << circle.area() << endl;
    cout << "Rectangle perimeter: " << rect.perimeter() << endl;
    
    return 0;
}
```

### `using` Declaration for Specific Members
```cpp
#include <iostream>
using namespace std;

namespace Math {
    double add(double a, double b) { return a + b; }
    double subtract(double a, double b) { return a - b; }
    double multiply(double a, double b) { return a * b; }
    double divide(double a, double b) { 
        if (b != 0) return a / b;
        return 0;
    }
}

namespace Constants {
    const double PI = 3.14159;
    const double E = 2.71828;
    const double GRAVITY = 9.81;
}

int main() {
    // Using specific members only
    using Math::add;
    using Math::multiply;
    using Constants::PI;
    
    // Now we can use them directly
    cout << "5 + 3 = " << add(5, 3) << endl;
    cout << "5 * 3 = " << multiply(5, 3) << endl;
    cout << "PI = " << PI << endl;
    
    // Still need scope resolution for other members
    cout << "5 - 3 = " << Math::subtract(5, 3) << endl;
    cout << "E = " << Constants::E << endl;
    
    return 0;
}
```

## 3. Namespace Scope and Organization

### Organizing Related Functionality
```cpp
#include <iostream>
#include <string>
#include <vector>
using namespace std;

namespace FileSystem {
    class File {
    private:
        string name;
        size_t size;
    public:
        File(string n, size_t s) : name(n), size(s) {}
        
        string getName() const { return name; }
        size_t getSize() const { return size; }
        
        void display() const {
            cout << "File: " << name << " (" << size << " bytes)" << endl;
        }
    };
    
    class Directory {
    private:
        string name;
        vector<File> files;
    public:
        Directory(string n) : name(n) {}
        
        void addFile(const File& file) {
            files.push_back(file);
        }
        
        void listFiles() const {
            cout << "Directory: " << name << endl;
            for (const auto& file : files) {
                file.display();
            }
        }
    };
    
    // Utility functions
    string getExtension(const string& filename) {
        size_t dotPos = filename.find_last_of('.');
        if (dotPos != string::npos) {
            return filename.substr(dotPos + 1);
        }
        return "";
    }
    
    bool isValidFilename(const string& filename) {
        return !filename.empty() && filename.length() <= 255;
    }
}

namespace Network {
    class Connection {
    private:
        string address;
        int port;
        bool connected;
    public:
        Connection(string addr, int p) : address(addr), port(p), connected(false) {}
        
        bool connect() {
            cout << "Connecting to " << address << ":" << port << endl;
            connected = true;
            return true;
        }
        
        void disconnect() {
            cout << "Disconnecting from " << address << ":" << port << endl;
            connected = false;
        }
        
        bool sendData(const string& data) {
            if (connected) {
                cout << "Sending data: " << data << endl;
                return true;
            }
            return false;
        }
    };
    
    // Protocol constants
    namespace Protocols {
        const int HTTP = 80;
        const int HTTPS = 443;
        const int FTP = 21;
        const int SSH = 22;
    }
}

int main() {
    // Using FileSystem namespace
    FileSystem::Directory docs("Documents");
    docs.addFile(FileSystem::File("report.pdf", 2048));
    docs.addFile(FileSystem::File("data.txt", 512));
    docs.listFiles();
    
    cout << "Extension of 'image.jpg': " << FileSystem::getExtension("image.jpg") << endl;
    
    // Using Network namespace
    Network::Connection conn("192.168.1.1", Network::Protocols::HTTP);
    conn.connect();
    conn.sendData("Hello Server!");
    conn.disconnect();
    
    return 0;
}
```

## 4. Nested Namespaces

### Basic Nested Namespaces
```cpp
#include <iostream>
#include <string>
using namespace std;

namespace Company {
    namespace HR {
        class Employee {
        private:
            string name;
            int id;
            double salary;
        public:
            Employee(string n, int i, double s) : name(n), id(i), salary(s) {}
            
            void display() const {
                cout << "Employee: " << name << " (ID: " << id 
                     << ", Salary: $" << salary << ")" << endl;
            }
        };
        
        void processPayroll() {
            cout << "Processing payroll..." << endl;
        }
    }
    
    namespace Finance {
        class Budget {
        private:
            double allocated;
            double spent;
        public:
            Budget(double alloc) : allocated(alloc), spent(0) {}
            
            bool spend(double amount) {
                if (spent + amount <= allocated) {
                    spent += amount;
                    return true;
                }
                return false;
            }
            
            double getRemaining() const {
                return allocated - spent;
            }
        };
        
        void generateReport() {
            cout << "Generating financial report..." << endl;
        }
    }
    
    namespace IT {
        namespace Security {
            class User {
            private:
                string username;
                string passwordHash;
            public:
                User(string user, string pass) : username(user), passwordHash(pass) {}
                
                bool authenticate(string password) const {
                    return passwordHash == password; // Simplified
                }
            };
            
            void auditAccess() {
                cout << "Auditing system access..." << endl;
            }
        }
        
        namespace Infrastructure {
            class Server {
            private:
                string hostname;
                bool running;
            public:
                Server(string host) : hostname(host), running(false) {}
                
                void start() {
                    running = true;
                    cout << "Server " << hostname << " started." << endl;
                }
                
                void stop() {
                    running = false;
                    cout << "Server " << hostname << " stopped." << endl;
                }
            };
        }
    }
}

int main() {
    // Using nested namespaces
    Company::HR::Employee emp("John Doe", 1001, 75000);
    emp.display();
    Company::HR::processPayroll();
    
    Company::Finance::Budget budget(50000);
    budget.spend(15000);
    cout << "Remaining budget: $" << budget.getRemaining() << endl;
    
    Company::IT::Security::User user("admin", "secret");
    if (user.authenticate("secret")) {
        cout << "Authentication successful!" << endl;
    }
    
    Company::IT::Infrastructure::Server server("web01");
    server.start();
    
    return 0;
}
```

## 5. Inline Namespaces (C++11)

### Versioning with Inline Namespaces
```cpp
#include <iostream>
using namespace std;

namespace Library {
    // Version 1.0
    namespace v1 {
        class Calculator {
        public:
            double add(double a, double b) {
                return a + b;
            }
            
            double multiply(double a, double b) {
                return a * b;
            }
        };
    }
    
    // Version 2.0 with new features
    inline namespace v2 {
        class Calculator {
        public:
            double add(double a, double b) {
                cout << "Using v2 add function" << endl;
                return a + b;
            }
            
            double multiply(double a, double b) {
                cout << "Using v2 multiply function" << endl;
                return a * b;
            }
            
            // New in v2
            double power(double base, double exponent) {
                double result = 1;
                for (int i = 0; i < exponent; i++) {
                    result *= base;
                }
                return result;
            }
        };
    }
    
    // Future version (not inline)
    namespace v3 {
        class Calculator {
        public:
            // Advanced implementation...
        };
    }
}

// Client code - uses the inline version by default
int main() {
    Library::Calculator calc;  // Uses v2 because it's inline
    
    cout << "5 + 3 = " << calc.add(5, 3) << endl;
    cout << "5 * 3 = " << calc.multiply(5, 3) << endl;
    cout << "2^4 = " << calc.power(2, 4) << endl;
    
    // Can still access specific versions
    Library::v1::Calculator oldCalc;
    cout << "Old version: 5 + 3 = " << oldCalc.add(5, 3) << endl;
    
    return 0;
}
```

## 6. Namespace Aliases

### Creating Aliases for Long Namespace Names
```cpp
#include <iostream>
#include <string>
using namespace std;

namespace VeryLongNamespaceNameThatIsHardToType {
    class ImportantClass {
    public:
        void importantMethod() {
            cout << "Important work done!" << endl;
        }
    };
    
    void usefulFunction() {
        cout << "Useful function called!" << endl;
    }
}

namespace AnotherVeryLongName {
    namespace NestedLongName {
        class ComplexClass {
        public:
            void complexOperation() {
                cout << "Complex operation performed!" << endl;
            }
        };
    }
}

int main() {
    // Create aliases for long namespace names
    namespace Short = VeryLongNamespaceNameThatIsHardToType;
    namespace NestedShort = AnotherVeryLongName::NestedLongName;
    
    // Use the aliases
    Short::ImportantClass obj1;
    obj1.importantMethod();
    Short::usefulFunction();
    
    NestedShort::ComplexClass obj2;
    obj2.complexOperation();
    
    // Temporary alias in a scope
    {
        namespace Calc = VeryLongNamespaceNameThatIsHardToType;
        Calc::ImportantClass tempObj;
        tempObj.importantMethod();
    }
    
    return 0;
}
```

## 7. Anonymous Namespaces

### File-Scope with Anonymous Namespaces
```cpp
#include <iostream>
using namespace std;

// Anonymous namespace - internal linkage
namespace {
    int internalVariable = 42;
    
    void internalFunction() {
        cout << "This is an internal function" << endl;
    }
    
    class InternalClass {
    public:
        void display() {
            cout << "Internal class, variable = " << internalVariable << endl;
        }
    };
}

// Regular global (external linkage)
int globalVariable = 100;

void regularFunction() {
    cout << "Regular function, can access internal: " << internalVariable << endl;
    internalFunction();
}

int main() {
    cout << "Internal variable: " << internalVariable << endl;
    internalFunction();
    
    InternalClass internalObj;
    internalObj.display();
    
    regularFunction();
    
    cout << "Global variable: " << globalVariable << endl;
    
    return 0;
}

// Another file would not see the anonymous namespace members
// They are effectively static to this translation unit
```

## 8. The `std` Namespace

### Working with Standard Library Namespace
```cpp
#include <iostream>
#include <vector>
#include <string>
#include <algorithm>

// Different ways to use std namespace

// Method 1: No using directive - always use std::
void method1() {
    std::cout << "Method 1: Always use std::" << std::endl;
    std::vector<int> numbers = {5, 2, 8, 1, 9};
    std::sort(numbers.begin(), numbers.end());
    
    for (std::vector<int>::iterator it = numbers.begin(); it != numbers.end(); ++it) {
        std::cout << *it << " ";
    }
    std::cout << std::endl;
}

// Method 2: Using directive in function scope
void method2() {
    using namespace std;
    
    cout << "Method 2: using namespace std in function" << endl;
    vector<string> names = {"Alice", "Bob", "Charlie"};
    
    for (const auto& name : names) {
        cout << name << " ";
    }
    cout << endl;
}

// Method 3: Using declarations for specific members
void method3() {
    using std::cout;
    using std::endl;
    using std::string;
    
    cout << "Method 3: Specific using declarations" << endl;
    string message = "Hello World";
    cout << message << endl;
}

// Method 4: Global using directive (generally not recommended)
// using namespace std;

int main() {
    method1();
    method2();
    method3();
    
    return 0;
}
```

## 9. Namespace Composition and Extension

### Extending Namespaces Across Files
```cpp
// math_operations.h
#ifndef MATH_OPERATIONS_H
#define MATH_OPERATIONS_H

namespace Math {
    // Basic operations
    double add(double a, double b);
    double subtract(double a, double b);
    double multiply(double a, double b);
    double divide(double a, double b);
}

#endif

// math_operations.cpp
#include "math_operations.h"

namespace Math {
    double add(double a, double b) {
        return a + b;
    }
    
    double subtract(double a, double b) {
        return a - b;
    }
    
    double multiply(double a, double b) {
        return a * b;
    }
    
    double divide(double a, double b) {
        if (b != 0) return a / b;
        return 0;
    }
}

// advanced_math.h
#ifndef ADVANCED_MATH_H
#define ADVANCED_MATH_H

namespace Math {
    // Extending the Math namespace
    double power(double base, double exponent);
    double squareRoot(double x);
    double factorial(int n);
}

#endif

// advanced_math.cpp
#include "advanced_math.h"
#include <cmath>

namespace Math {
    double power(double base, double exponent) {
        return std::pow(base, exponent);
    }
    
    double squareRoot(double x) {
        if (x >= 0) return std::sqrt(x);
        return 0;
    }
    
    double factorial(int n) {
        if (n <= 1) return 1;
        double result = 1;
        for (int i = 2; i <= n; i++) {
            result *= i;
        }
        return result;
    }
}

// main.cpp
#include <iostream>
#include "math_operations.h"
#include "advanced_math.h"

int main() {
    using std::cout;
    using std::endl;
    
    cout << "Basic Math Operations:" << endl;
    cout << "5 + 3 = " << Math::add(5, 3) << endl;
    cout << "5 * 3 = " << Math::multiply(5, 3) << endl;
    
    cout << "\nAdvanced Math Operations:" << endl;
    cout << "2^4 = " << Math::power(2, 4) << endl;
    cout << "sqrt(16) = " << Math::squareRoot(16) << endl;
    cout << "5! = " << Math::factorial(5) << endl;
    
    return 0;
}
```

## 10. Advanced Namespace Features

### Namespace Composition and ADL (Argument-Dependent Lookup)
```cpp
#include <iostream>
#include <string>
using namespace std;

namespace Graphics {
    class Point {
    public:
        double x, y;
        
        Point(double x = 0, double y = 0) : x(x), y(y) {}
    };
    
    // Operator overload in same namespace as operands (enables ADL)
    Point operator+(const Point& a, const Point& b) {
        return Point(a.x + b.x, a.y + b.y);
    }
    
    ostream& operator<<(ostream& os, const Point& p) {
        os << "(" << p.x << ", " << p.y << ")";
        return os;
    }
}

namespace Math {
    class Vector {
    public:
        double x, y;
        
        Vector(double x = 0, double y = 0) : x(x), y(y) {}
    };
}

// ADL in action
void demonstrateADL() {
    Graphics::Point p1(1, 2), p2(3, 4);
    
    // ADL finds operator+ in Graphics namespace
    Graphics::Point p3 = p1 + p2;
    
    // ADL finds operator<< in Graphics namespace
    cout << "p1 = " << p1 << endl;
    cout << "p2 = " << p2 << endl;
    cout << "p1 + p2 = " << p3 << endl;
}

// Namespace composition
namespace Company {
    namespace Department {
        namespace Team {
            class Member {
            public:
                string name;
                Member(string n) : name(n) {}
            };
        }
    }
}

// C++17 nested namespace definition
namespace Company::Department::Team::Utils {
    void logMember(const Member& m) {
        cout << "Member: " << m.name << endl;
    }
}

int main() {
    demonstrateADL();
    
    // Using nested namespaces (C++17 style)
    Company::Department::Team::Member member("Alice");
    Company::Department::Team::Utils::logMember(member);
    
    return 0;
}
```

## 11. Comprehensive Example: Game Engine Namespaces

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <memory>
using namespace std;

namespace GameEngine {
    namespace Core {
        class GameObject {
        protected:
            string name;
            bool active;
        public:
            GameObject(string n) : name(n), active(true) {}
            
            virtual void update() = 0;
            virtual void render() = 0;
            
            void setActive(bool isActive) { active = isActive; }
            bool isActive() const { return active; }
            string getName() const { return name; }
            
            virtual ~GameObject() = default;
        };
        
        class Scene {
        private:
            string name;
            vector<unique_ptr<GameObject>> objects;
        public:
            Scene(string n) : name(n) {}
            
            void addObject(unique_ptr<GameObject> obj) {
                objects.push_back(move(obj));
            }
            
            void updateAll() {
                for (auto& obj : objects) {
                    if (obj->isActive()) {
                        obj->update();
                    }
                }
            }
            
            void renderAll() {
                for (auto& obj : objects) {
                    if (obj->isActive()) {
                        obj->render();
                    }
                }
            }
        };
    }
    
    namespace Graphics {
        class Renderer {
        public:
            void clearScreen() {
                cout << "Clearing screen..." << endl;
            }
            
            void drawSprite(string sprite, int x, int y) {
                cout << "Drawing " << sprite << " at (" << x << ", " << y << ")" << endl;
            }
            
            void present() {
                cout << "Presenting frame..." << endl;
            }
        };
        
        class Sprite : public Core::GameObject {
        private:
            string texture;
            int x, y;
        public:
            Sprite(string n, string tex, int posX, int posY) 
                : Core::GameObject(n), texture(tex), x(posX), y(posY) {}
            
            void update() override {
                cout << "Updating sprite: " << getName() << endl;
            }
            
            void render() override {
                cout << "Rendering sprite: " << getName() << " with texture: " << texture << endl;
            }
        };
    }
    
    namespace Audio {
        class SoundPlayer {
        public:
            void playSound(string sound) {
                cout << "Playing sound: " << sound << endl;
            }
            
            void stopAllSounds() {
                cout << "Stopping all sounds" << endl;
            }
        };
        
        class BackgroundMusic : public Core::GameObject {
        private:
            string musicTrack;
            bool playing;
        public:
            BackgroundMusic(string n, string track) 
                : Core::GameObject(n), musicTrack(track), playing(false) {}
            
            void update() override {
                if (!playing) {
                    cout << "Starting background music: " << musicTrack << endl;
                    playing = true;
                }
            }
            
            void render() override {
                // Music doesn't render visually
            }
        };
    }
    
    namespace Physics {
        class Collider {
        public:
            bool checkCollision(int x1, int y1, int x2, int y2) {
                // Simple collision detection
                return (x1 == x2 && y1 == y2);
            }
        };
        
        class PhysicsObject : public Core::GameObject {
        private:
            int velocityX, velocityY;
        public:
            PhysicsObject(string n, int vx, int vy) 
                : Core::GameObject(n), velocityX(vx), velocityY(vy) {}
            
            void update() override {
                cout << "Updating physics for: " << getName() 
                     << " (velocity: " << velocityX << ", " << velocityY << ")" << endl;
            }
            
            void render() override {
                cout << "Rendering physics object: " << getName() << endl;
            }
        };
    }
    
    // Utility namespace
    namespace Utils {
        class Random {
        public:
            static int range(int min, int max) {
                return min + rand() % (max - min + 1);
            }
        };
        
        class Timer {
        private:
            long startTime;
        public:
            void start() {
                startTime = time(nullptr);
            }
            
            long getElapsed() const {
                return time(nullptr) - startTime;
            }
        };
    }
}

// Using the game engine
int main() {
    using namespace GameEngine;
    
    // Create a scene
    Core::Scene mainScene("Main Scene");
    
    // Add game objects
    mainScene.addObject(make_unique<Graphics::Sprite>("Player", "player.png", 100, 100));
    mainScene.addObject(make_unique<Graphics::Sprite>("Enemy", "enemy.png", 200, 150));
    mainScene.addObject(make_unique<Audio::BackgroundMusic>("BGM", "theme.mp3"));
    mainScene.addObject(make_unique<Physics::PhysicsObject>("Ball", 5, 10));
    
    // Game loop simulation
    Graphics::Renderer renderer;
    
    for (int frame = 0; frame < 3; frame++) {
        cout << "\n--- Frame " << frame << " ---" << endl;
        
        renderer.clearScreen();
        mainScene.updateAll();
        mainScene.renderAll();
        renderer.present();
    }
    
    return 0;
}
```