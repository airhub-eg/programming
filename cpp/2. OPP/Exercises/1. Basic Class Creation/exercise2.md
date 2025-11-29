# Exercise 2: BankAccount Class
Create a `BankAccount` class with:
- Private members: accountNumber, accountHolder, balance
- Constructor to initialize account details
- Methods: `deposit(amount)`, `withdraw(amount)`, `checkBalance()`
- Ensure withdrawal doesn't make balance negative
- Create 2 accounts, perform transactions, and display balances

**Solution:**
<details> <summary>Solution</summary>

```cpp
#include <iostream>
#include <string>
using namespace std;

class BankAccount {
private:
    int accountNumber;
    string accountHolder;
    double balance;

public:
    // Constructor
    BankAccount(int accNum, string holder, double initialBalance) {
        accountNumber = accNum;
        accountHolder = holder;
        balance = initialBalance >= 0 ? initialBalance : 0;
    }

    // Deposit method
    void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            cout << "Deposited: $" << amount << endl;
            cout << "New Balance: $" << balance << endl;
        } else {
            cout << "Invalid deposit amount!" << endl;
        }
    }

    // Withdraw method
    void withdraw(double amount) {
        if (amount > 0) {
            if (amount <= balance) {
                balance -= amount;
                cout << "Withdrawn: $" << amount << endl;
                cout << "New Balance: $" << balance << endl;
            } else {
                cout << "Insufficient balance! Current balance: $" << balance << endl;
            }
        } else {
            cout << "Invalid withdrawal amount!" << endl;
        }
    }

    // Check balance method
    void checkBalance() {
        cout << "Account Number: " << accountNumber << endl;
        cout << "Account Holder: " << accountHolder << endl;
        cout << "Current Balance: $" << balance << endl;
    }

    // Display account details
    void displayAccount() {
        cout << "\n--- Account Details ---" << endl;
        checkBalance();
    }
};

int main() {
    // Creating 2 bank accounts
    BankAccount account1(1001, "John Smith", 5000.0);
    BankAccount account2(1002, "Jane Doe", 3000.0);

    // Display initial account information
    account1.displayAccount();
    account2.displayAccount();

    // Perform transactions on account 1
    cout << "\n--- Transactions for Account 1 ---" << endl;
    account1.deposit(1500);
    account1.withdraw(2000);
    account1.withdraw(10000); // Should fail

    // Perform transactions on account 2
    cout << "\n--- Transactions for Account 2 ---" << endl;
    account2.deposit(500);
    account2.withdraw(1000);

    // Display final balances
    cout << "\n--- Final Account Status ---" << endl;
    account1.displayAccount();
    account2.displayAccount();

    return 0;
}
```

</details>
