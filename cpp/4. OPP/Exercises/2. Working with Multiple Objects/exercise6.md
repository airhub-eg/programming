# Exercise 6: Product Inventory
Create a `Product` class with:
- Private members: productID, name, quantity, price
- Constructor
- Methods: `addStock(amount)`, `sellProduct(amount)`, `calculateValue()` (quantity × price)
- Method `isInStock()` returns true if quantity > 0
- Create 10 products, perform various stock operations, calculate total inventory value

**Solution:**
<details> <summary>Solution</summary>

```cpp
#include <iostream>
#include <string>
using namespace std;

class Product {
private:
    int productID;
    string name;
    int quantity;
    double price;

public:
    // Constructor
    Product(int id, string n, int qty, double p) {
        productID = id;
        name = n;
        quantity = qty;
        price = p;
    }

    // Add stock
    void addStock(int amount) {
        if (amount > 0) {
            quantity += amount;
            cout << amount << " units added to " << name << endl;
            cout << "New quantity: " << quantity << endl;
        } else {
            cout << "Invalid amount!" << endl;
        }
    }

    // Sell product
    void sellProduct(int amount) {
        if (amount > 0) {
            if (amount <= quantity) {
                quantity -= amount;
                cout << amount << " units of " << name << " sold" << endl;
                cout << "Remaining quantity: " << quantity << endl;
            } else {
                cout << "Not enough stock! Available: " << quantity << endl;
            }
        } else {
            cout << "Invalid amount!" << endl;
        }
    }

    // Calculate total value
    double calculateValue() {
        return quantity * price;
    }

    // Check if in stock
    bool isInStock() {
        return quantity > 0;
    }

    // Display product information
    void displayInfo() {
        cout << "\nProduct ID: " << productID << endl;
        cout << "Name: " << name << endl;
        cout << "Quantity: " << quantity << endl;
        cout << "Price: $" << price << endl;
        cout << "Total Value: $" << calculateValue() << endl;
        cout << "Status: " << (isInStock() ? "In Stock" : "Out of Stock") << endl;
    }
};

int main() {
    // Creating 10 products
    Product products[10] = {
        Product(1, "Laptop", 50, 999.99),
        Product(2, "Mouse", 200, 19.99),
        Product(3, "Keyboard", 150, 49.99),
        Product(4, "Monitor", 75, 299.99),
        Product(5, "Headphones", 120, 79.99),
        Product(6, "Webcam", 60, 89.99),
        Product(7, "USB Cable", 300, 9.99),
        Product(8, "External HDD", 40, 129.99),
        Product(9, "Speaker", 80, 149.99),
        Product(10, "Tablet", 30, 499.99)
    };

    // Display all products
    cout << "========== INITIAL INVENTORY ==========" << endl;
    for (int i = 0; i < 10; i++) {
        products[i].displayInfo();
    }

    // Perform various stock operations
    cout << "\n========== STOCK OPERATIONS ==========" << endl;
    products[0].sellProduct(10);  // Sell 10 laptops
    products[1].addStock(50);     // Add 50 mice
    products[2].sellProduct(30);  // Sell 30 keyboards
    products[5].sellProduct(100); // Try to sell more than available
    products[7].addStock(25);     // Add stock to external HDD

    // Calculate total inventory value
    cout << "\n========== INVENTORY SUMMARY ==========" << endl;
    double totalValue = 0;
    int inStockCount = 0;

    for (int i = 0; i < 10; i++) {
        totalValue += products[i].calculateValue();
        if (products[i].isInStock()) {
            inStockCount++;
        }
    }

    cout << "Total Inventory Value: $" << totalValue << endl;
    cout << "Products In Stock: " << inStockCount << " out of 10" << endl;

    // Display updated inventory
    cout << "\n========== UPDATED INVENTORY ==========" << endl;
    for (int i = 0; i < 10; i++) {
        products[i].displayInfo();
    }

    return 0;
}
```

</details>