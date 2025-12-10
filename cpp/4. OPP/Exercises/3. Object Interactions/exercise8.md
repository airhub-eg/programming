# Exercise 8: Library Management
Create two classes:
- `Book` class: bookID, title, author, isIssued (bool)
- `Library` class: array of Books (max 100), bookCount
- Methods in Library: `addBook()`, `issueBook(bookID)`, `returnBook(bookID)`, `searchByAuthor()`, `displayAvailableBooks()`
- Simulate library operations

**Solution:**
<details> <summary>Solution</summary>

```cpp
#include <iostream>
#include <string>
using namespace std;

class Book {
private:
    int bookID;
    string title;
    string author;
    bool isIssued;

public:
    // Constructor
    Book(int id = 0, string t = "", string a = "", bool issued = false) {
        bookID = id;
        title = t;
        author = a;
        isIssued = issued;
    }

    // Getters
    int getBookID() {
        return bookID;
    }

    string getTitle() {
        return title;
    }

    string getAuthor() {
        return author;
    }

    bool getIssuedStatus() {
        return isIssued;
    }

    // Setters
    void setIssuedStatus(bool status) {
        isIssued = status;
    }

    // Display book
    void display() {
        cout << "ID: " << bookID << " | Title: " << title 
             << " | Author: " << author 
             << " | Status: " << (isIssued ? "Issued" : "Available") << endl;
    }
};

class Library {
private:
    Book books[100];
    int bookCount;

public:
    // Constructor
    Library() {
        bookCount = 0;
    }

    // Add book
    void addBook(int id, string title, string author) {
        if (bookCount < 100) {
            books[bookCount] = Book(id, title, author, false);
            bookCount++;
            cout << "Book added: " << title << endl;
        } else {
            cout << "Library is full!" << endl;
        }
    }

    // Issue book
    void issueBook(int bookID) {
        bool found = false;
        for (int i = 0; i < bookCount; i++) {
            if (books[i].getBookID() == bookID) {
                found = true;
                if (!books[i].getIssuedStatus()) {
                    books[i].setIssuedStatus(true);
                    cout << "Book issued: " << books[i].getTitle() << endl;
                } else {
                    cout << "Book already issued!" << endl;
                }
                break;
            }
        }
        if (!found) {
            cout << "Book not found!" << endl;
        }
    }

    // Return book
    void returnBook(int bookID) {
        bool found = false;
        for (int i = 0; i < bookCount; i++) {
            if (books[i].getBookID() == bookID) {
                found = true;
                if (books[i].getIssuedStatus()) {
                    books[i].setIssuedStatus(false);
                    cout << "Book returned: " << books[i].getTitle() << endl;
                } else {
                    cout << "Book was not issued!" << endl;
                }
                break;
            }
        }
        if (!found) {
            cout << "Book not found!" << endl;
        }
    }

    // Search by author
    void searchByAuthor(string author) {
        cout << "\n--- Books by " << author << " ---" << endl;
        bool found = false;
        for (int i = 0; i < bookCount; i++) {
            if (books[i].getAuthor() == author) {
                books[i].display();
                found = true;
            }
        }
        if (!found) {
            cout << "No books found by this author." << endl;
        }
    }

    // Display available books
    void displayAvailableBooks() {
        cout << "\n========== AVAILABLE BOOKS ==========" << endl;
        bool hasAvailable = false;
        for (int i = 0; i < bookCount; i++) {
            if (!books[i].getIssuedStatus()) {
                books[i].display();
                hasAvailable = true;
            }
        }
        if (!hasAvailable) {
            cout << "No books available." << endl;
        }
        cout << "=====================================" << endl;
    }

    // Display all books
    void displayAllBooks() {
        cout << "\n========== ALL BOOKS ==========" << endl;
        for (int i = 0; i < bookCount; i++) {
            books[i].display();
        }
        cout << "===============================" << endl;
    }
};

int main() {
    Library lib;

    // Add books to library
    cout << "========== ADDING BOOKS ==========" << endl;
    lib.addBook(101, "The Great Gatsby", "F. Scott Fitzgerald");
    lib.addBook(102, "1984", "George Orwell");
    lib.addBook(103, "To Kill a Mockingbird", "Harper Lee");
    lib.addBook(104, "Animal Farm", "George Orwell");
    lib.addBook(105, "Pride and Prejudice", "Jane Austen");

    // Display all books
    lib.displayAllBooks();

    // Issue some books
    cout << "\n========== ISSUING BOOKS ==========" << endl;
    lib.issueBook(101);
    lib.issueBook(103);
    lib.issueBook(103);  // Try to issue already issued book

    // Display available books
    lib.displayAvailableBooks();

    // Search by author
    lib.searchByAuthor("George Orwell");

    // Return a book
    cout << "\n========== RETURNING BOOK ==========" << endl;
    lib.returnBook(101);

    // Display available books again
    lib.displayAvailableBooks();

    // Display all books
    lib.displayAllBooks();

    return 0;
}
```

</details>