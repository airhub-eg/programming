# Exercise 7: Shopping Cart
Create two classes:
- `Item` class: name, price, quantity
- `ShoppingCart` class: array of Items (max 10), itemCount
- Methods in ShoppingCart: `addItem()`, `removeItem()`, `calculateTotal()`, `displayCart()`
- Create a shopping scenario with multiple items

**Solution:**
<details> <summary>Solution</summary>

```cpp
#include <iostream>
#include <string>
using namespace std;

class Item {
private:
    string name;
    double price;
    int quantity;

public:
    // Constructor
    Item(string n = "", double p = 0.0, int q = 0) {
        name = n;
        price = p;
        quantity = q;
    }

    // Getters
    string getName() {
        return name;
    }

    double getPrice() {
        return price;
    }

    int getQuantity() {
        return quantity;
    }

    // Calculate item total
    double getTotal() {
        return price * quantity;
    }

    // Display item
    void display() {
        cout << name << " - $" << price << " x " << quantity 
             << " = $" << getTotal() << endl;
    }
};

class ShoppingCart {
private:
    Item items[10];
    int itemCount;

public:
    // Constructor
    ShoppingCart() {
        itemCount = 0;
    }

    // Add item to cart
    void addItem(string name, double price, int quantity) {
        if (itemCount < 10) {
            items[itemCount] = Item(name, price, quantity);
            itemCount++;
            cout << quantity << " x " << name << " added to cart" << endl;
        } else {
            cout << "Cart is full! Cannot add more items." << endl;
        }
    }

    // Remove item from cart
    void removeItem(string name) {
        bool found = false;
        for (int i = 0; i < itemCount; i++) {
            if (items[i].getName() == name) {
                found = true;
                // Shift remaining items
                for (int j = i; j < itemCount - 1; j++) {
                    items[j] = items[j + 1];
                }
                itemCount--;
                cout << name << " removed from cart" << endl;
                break;
            }
        }
        if (!found) {
            cout << name << " not found in cart" << endl;
        }
    }

    // Calculate total
    double calculateTotal() {
        double total = 0;
        for (int i = 0; i < itemCount; i++) {
            total += items[i].getTotal();
        }
        return total;
    }

    // Display cart
    void displayCart() {
        cout << "\n========== SHOPPING CART ==========" << endl;
        if (itemCount == 0) {
            cout << "Cart is empty!" << endl;
        } else {
            for (int i = 0; i < itemCount; i++) {
                cout << (i + 1) << ". ";
                items[i].display();
            }
            cout << "\nTotal: $" << calculateTotal() << endl;
        }
        cout << "===================================" << endl;
    }
};

int main() {
    ShoppingCart cart;

    // Shopping scenario
    cout << "========== SHOPPING SESSION ==========" << endl;
    
    // Add items to cart
    cart.addItem("Wireless Mouse", 29.99, 1);
    cart.addItem("USB Cable", 9.99, 2);
    cart.addItem("Keyboard", 59.99, 1);
    cart.addItem("Monitor", 299.99, 1);
    cart.addItem("HDMI Cable", 14.99, 3);

    // Display cart
    cart.displayCart();

    // Remove an item
    cout << "\n========== REMOVING ITEM ==========" << endl;
    cart.removeItem("USB Cable");

    // Display updated cart
    cart.displayCart();

    // Add more items
    cout << "\n========== ADDING MORE ITEMS ==========" << endl;
    cart.addItem("Webcam", 89.99, 1);
    cart.addItem("Headphones", 79.99, 2);

    // Final cart
    cart.displayCart();

    // Try to remove non-existent item
    cout << "\n========== REMOVING NON-EXISTENT ITEM ==========" << endl;
    cart.removeItem("Tablet");

    return 0;
}
```

</details>