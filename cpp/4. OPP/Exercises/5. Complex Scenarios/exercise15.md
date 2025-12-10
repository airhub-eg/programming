# Exercise 15: Traffic Signal Simulation
Create a `TrafficLight` class with:
- Private members: currentColor (red/yellow/green), timer
- Methods: `changeSignal()`, `getWaitTime()`, `displayStatus()`
- Static member to count total signal changes
- Create 4 traffic lights (intersection), simulate signal changes every few seconds

**Solution:**
<details> <summary>Solution</summary>

```cpp
#include <iostream>
#include <string>
using namespace std;

class TrafficLight {
private:
    string currentColor;
    int timer;
    string location;
    static int totalSignalChanges;

public:
    // Constructor
    TrafficLight(string loc = "Intersection") {
        location = loc;
        currentColor = "red";
        timer = 30;  // Default 30 seconds
    }

    // Change signal
    void changeSignal() {
        if (currentColor == "red") {
            currentColor = "green";
            timer = 45;
        } else if (currentColor == "green") {
            currentColor = "yellow";
            timer = 5;
        } else if (currentColor == "yellow") {
            currentColor = "red";
            timer = 30;
        }
        totalSignalChanges++;
    }

    // Get wait time based on current color
    int getWaitTime() {
        return timer;
    }

    // Display status
    void displayStatus() {
        cout << "[" << location << "] ";
        
        // Color-coded display
        if (currentColor == "red") {
            cout << "🔴 RED";
        } else if (currentColor == "yellow") {
            cout << "🟡 YELLOW";
        } else {
            cout << "🟢 GREEN";
        }
        
        cout << " - " << timer << " seconds remaining" << endl;
    }

    // Tick timer (decrease by 1 second)
    void tick() {
        if (timer > 0) {
            timer--;
        }
        if (timer == 0) {
            changeSignal();
        }
    }

    // Get static variable
    static int getTotalSignalChanges() {
        return totalSignalChanges;
    }

    // Getters
    string getCurrentColor() { return currentColor; }
    string getLocation() { return location; }
};

// Initialize static member
int TrafficLight::totalSignalChanges = 0;

int main() {
    // Create 4 traffic lights for an intersection
    TrafficLight lights[4] = {
        TrafficLight("North"),
        TrafficLight("South"),
        TrafficLight("East"),
        TrafficLight("West")
    };

    // Set initial states (alternate)
    lights[0].changeSignal();  // North - Green
    lights[1].changeSignal();  // South - Green
    // East and West stay Red

    cout << "========== TRAFFIC SIGNAL SIMULATION ==========" << endl;
    cout << "Simulating 4-way intersection with traffic lights\n" << endl;

    // Simulate for 2 minutes (120 seconds)
    const int SIMULATION_TIME = 120;
    
    for (int second = 1; second <= SIMULATION_TIME; second++) {
        // Display every 5 seconds
        if (second % 5 == 0 || second == 1) {
            cout << "\n--- Time: " << second << " seconds ---" << endl;
            for (int i = 0; i < 4; i++) {
                lights[i].displayStatus();
            }
        }

        // Tick all lights
        for (int i = 0; i < 4; i++) {
            lights[i].tick();
        }

        // Synchronize opposite lights
        // If North/South change, check if East/West should also change
        if (second % 80 == 0) {  // Every 80 seconds, swap which pair is green
            cout << "\n*** SWITCHING TRAFFIC FLOW ***" << endl;
        }
    }

    // Final status
    cout << "\n========== FINAL STATUS ==========" << endl;
    for (int i = 0; i < 4; i++) {
        lights[i].displayStatus();
    }

    // Statistics
    cout << "\n========== STATISTICS ==========" << endl;
    cout << "Total Simulation Time: " << SIMULATION_TIME << " seconds" << endl;
    cout << "Total Signal Changes: " << TrafficLight::getTotalSignalChanges() << endl;
    cout << "Average Changes per Light: " 
         << (TrafficLight::getTotalSignalChanges() / 4.0) << endl;

    // Demonstrate manual control
    cout << "\n========== MANUAL SIGNAL CONTROL TEST ==========" << endl;
    TrafficLight testLight("Test Intersection");
    
    cout << "Initial state: ";
    testLight.displayStatus();
    
    for (int i = 0; i < 5; i++) {
        testLight.changeSignal();
        cout << "After change " << (i + 1) << ": ";
        testLight.displayStatus();
    }

    cout << "\nTotal signal changes across all lights: " 
         << TrafficLight::getTotalSignalChanges() << endl;

    return 0;
}
```

</details>