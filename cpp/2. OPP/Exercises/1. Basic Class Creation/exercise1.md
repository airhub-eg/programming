# Exercise 1: Book Class
Create a `Book` class with:
- Private members: title, author, price, pages
- Constructor to initialize all members
- Getter and setter methods for all members
- A method `displayInfo()` to show all book details
- Create 3 book objects and display their information

**Solution:**
<details> <summary>Solution</summary>

```cpp
#include <iostream>
#include <string>
using namespace std;

class Book {
private:
    string title;
    string author;
    double price;
    int pages;

public:
    // Constructor
    Book(string t, string a, double p, int pg) {
        title = t;
        author = a;
        price = p;
        pages = pg;
    }

    // Setters
    void setTitle(string t) {
        title = t;
    }

    void setAuthor(string a) {
        author = a;
    }

    void setPrice(double p) {
        if (p >= 0) {
            price = p;
        } else {
            cout << "Price cannot be negative!" << endl;
        }
    }

    void setPages(int pg) {
        if (pg > 0) {
            pages = pg;
        } else {
            cout << "Pages must be positive!" << endl;
        }
    }

    // Getters
    string getTitle() {
        return title;
    }

    string getAuthor() {
        return author;
    }

    double getPrice() {
        return price;
    }

    int getPages() {
        return pages;
    }

    // Display method
    void displayInfo() {
        cout << "\n--- Book Information ---" << endl;
        cout << "Title: " << title << endl;
        cout << "Author: " << author << endl;
        cout << "Price: $" << price << endl;
        cout << "Pages: " << pages << endl;
    }
};

int main() {
    // Creating 3 book objects
    Book book1("The Great Gatsby", "F. Scott Fitzgerald", 15.99, 180);
    Book book2("1984", "George Orwell", 18.50, 328);
    Book book3("To Kill a Mockingbird", "Harper Lee", 14.99, 281);

    // Display information for all books
    book1.displayInfo();
    book2.displayInfo();
    book3.displayInfo();

    // Testing setters
    cout << "\n--- Updating Book 1 Price ---" << endl;
    book1.setPrice(12.99);
    book1.displayInfo();

    return 0;
}
```

</details>