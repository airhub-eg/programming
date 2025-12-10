# Exercise 13: Hotel Reservation System
Create two classes:
- `Room` class: roomNumber, type (single/double/suite), pricePerNight, isOccupied
- `Hotel` class: array of Rooms, hotelName
- Methods: `bookRoom(type)`, `checkOut(roomNumber)`, `displayAvailableRooms()`, `calculateRevenue()`
- Simulate hotel operations over multiple days

**Solution:**
<details> <summary>Solution</summary>

```cpp
#include <iostream>
#include <string>
using namespace std;

class Room {
private:
    int roomNumber;
    string type;  // single, double, suite
    double pricePerNight;
    bool isOccupied;

public:
    // Constructor
    Room(int num = 0, string t = "single", double price = 0.0) {
        roomNumber = num;
        type = t;
        pricePerNight = price;
        isOccupied = false;
    }

    // Book room
    bool book() {
        if (!isOccupied) {
            isOccupied = true;
            return true;
        }
        return false;
    }

    // Checkout
    void checkout() {
        isOccupied = false;
    }

    // Getters
    int getRoomNumber() { return roomNumber; }
    string getType() { return type; }
    double getPricePerNight() { return pricePerNight; }
    bool getOccupied() { return isOccupied; }

    // Display room info
    void display() {
        cout << "Room " << roomNumber << " | Type: " << type 
             << " | Price: $" << pricePerNight << "/night | Status: "
             << (isOccupied ? "Occupied" : "Available") << endl;
    }
};

class Hotel {
private:
    Room rooms[20];
    int roomCount;
    string hotelName;
    double totalRevenue;

public:
    // Constructor
    Hotel(string name) {
        hotelName = name;
        roomCount = 0;
        totalRevenue = 0.0;
    }

    // Add room to hotel
    void addRoom(int roomNum, string type, double price) {
        if (roomCount < 20) {
            rooms[roomCount] = Room(roomNum, type, price);
            roomCount++;
        }
    }

    // Book room by type
    int bookRoom(string type) {
        for (int i = 0; i < roomCount; i++) {
            if (rooms[i].getType() == type && !rooms[i].getOccupied()) {
                rooms[i].book();
                cout << "Room " << rooms[i].getRoomNumber() 
                     << " booked successfully!" << endl;
                return rooms[i].getRoomNumber();
            }
        }
        cout << "No available " << type << " rooms!" << endl;
        return -1;
    }

    // Checkout room
    void checkOut(int roomNumber, int nights) {
        for (int i = 0; i < roomCount; i++) {
            if (rooms[i].getRoomNumber() == roomNumber) {
                if (rooms[i].getOccupied()) {
                    double bill = rooms[i].getPricePerNight() * nights;
                    totalRevenue += bill;
                    rooms[i].checkout();
                    cout << "Room " << roomNumber << " checked out." << endl;
                    cout << "Bill for " << nights << " nights: $" << bill << endl;
                } else {
                    cout << "Room " << roomNumber << " is not occupied!" << endl;
                }
                return;
            }
        }
        cout << "Room number not found!" << endl;
    }

    // Display available rooms
    void displayAvailableRooms() {
        cout << "\n--- Available Rooms in " << hotelName << " ---" << endl;
        bool hasAvailable = false;
        for (int i = 0; i < roomCount; i++) {
            if (!rooms[i].getOccupied()) {
                rooms[i].display();
                hasAvailable = true;
            }
        }
        if (!hasAvailable) {
            cout << "No rooms available!" << endl;
        }
    }

    // Display all rooms
    void displayAllRooms() {
        cout << "\n--- All Rooms in " << hotelName << " ---" << endl;
        for (int i = 0; i < roomCount; i++) {
            rooms[i].display();
        }
    }

    // Calculate revenue
    double calculateRevenue() {
        return totalRevenue;
    }

    // Display hotel statistics
    void displayStatistics() {
        int occupied = 0;
        int available = 0;
        
        for (int i = 0; i < roomCount; i++) {
            if (rooms[i].getOccupied()) {
                occupied++;
            } else {
                available++;
            }
        }

        cout << "\n========== " << hotelName << " STATISTICS ==========" << endl;
        cout << "Total Rooms: " << roomCount << endl;
        cout << "Occupied: " << occupied << endl;
        cout << "Available: " << available << endl;
        cout << "Occupancy Rate: " << (occupied * 100.0 / roomCount) << "%" << endl;
        cout << "Total Revenue: $" << totalRevenue << endl;
    }
};

int main() {
    // Create hotel
    Hotel hotel("Grand Plaza Hotel");

    // Add rooms
    hotel.addRoom(101, "single", 100.0);
    hotel.addRoom(102, "single", 100.0);
    hotel.addRoom(103, "single", 100.0);
    hotel.addRoom(201, "double", 150.0);
    hotel.addRoom(202, "double", 150.0);
    hotel.addRoom(203, "double", 150.0);
    hotel.addRoom(301, "suite", 300.0);
    hotel.addRoom(302, "suite", 300.0);

    cout << "========== HOTEL SYSTEM INITIALIZED ==========" << endl;
    hotel.displayAllRooms();

    // Day 1: Bookings
    cout << "\n========== DAY 1: BOOKINGS ==========" << endl;
    hotel.bookRoom("single");
    hotel.bookRoom("double");
    hotel.bookRoom("suite");
    hotel.bookRoom("single");

    hotel.displayAvailableRooms();

    // Day 2: More bookings
    cout << "\n========== DAY 2: MORE BOOKINGS ==========" << endl;
    hotel.bookRoom("double");
    hotel.bookRoom("single");

    hotel.displayStatistics();

    // Day 3: Checkouts
    cout << "\n========== DAY 3: CHECKOUTS ==========" << endl;
    hotel.checkOut(101, 2);  // 2 nights
    hotel.checkOut(201, 3);  // 3 nights
    hotel.checkOut(301, 1);  // 1 night

    hotel.displayAvailableRooms();

    // Day 4: More operations
    cout << "\n========== DAY 4: MORE OPERATIONS ==========" << endl;
    hotel.bookRoom("suite");
    hotel.bookRoom("double");
    hotel.checkOut(102, 3);

    // Final statistics
    cout << "\n========== FINAL REPORT ==========" << endl;
    hotel.displayAllRooms();
    hotel.displayStatistics();

    return 0;
}
```

</details>