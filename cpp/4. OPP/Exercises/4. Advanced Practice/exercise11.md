# Exercise 11: Bank System with Transactions
Create a `BankAccount` class with:
- Private members: accountNumber, name, balance, transactionHistory (array of last 10 transactions)
- Methods: `deposit()`, `withdraw()`, `transfer(BankAccount& other, amount)`
- Method `displayTransactionHistory()`
- Method `calculateInterest(rate)` for savings accounts
- Create multiple accounts and perform inter-account transfers

**Solution:**
<details> <summary>Solution</summary>

```cpp
#include <iostream>
#include <string>
using namespace std;

class BankAccount {
private:
    int accountNumber;
    string name;
    double balance;
    string transactionHistory[10];
    int transactionCount;

    // Add transaction to history
    void addTransaction(string transaction) {
        if (transactionCount < 10) {
            transactionHistory[transactionCount] = transaction;
            transactionCount++;
        } else {
            // Shift transactions and add new one
            for (int i = 0; i < 9; i++) {
                transactionHistory[i] = transactionHistory[i + 1];
            }
            transactionHistory[9] = transaction;
        }
    }

public:
    // Constructor
    BankAccount(int accNum, string n, double initialBalance) {
        accountNumber = accNum;
        name = n;
        balance = initialBalance >= 0 ? initialBalance : 0;
        transactionCount = 0;
        addTransaction("Account opened with balance: $" + to_string(balance));
    }

    // Deposit
    void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            addTransaction("Deposited: $" + to_string(amount));
            cout << "Deposited $" << amount << " to account " << accountNumber << endl;
        } else {
            cout << "Invalid deposit amount!" << endl;
        }
    }

    // Withdraw
    void withdraw(double amount) {
        if (amount > 0) {
            if (amount <= balance) {
                balance -= amount;
                addTransaction("Withdrew: $" + to_string(amount));
                cout << "Withdrew $" << amount << " from account " << accountNumber << endl;
            } else {
                cout << "Insufficient balance!" << endl;
            }
        } else {
            cout << "Invalid withdrawal amount!" << endl;
        }
    }

    // Transfer to another account
    void transfer(BankAccount& other, double amount) {
        if (amount > 0) {
            if (amount <= balance) {
                balance -= amount;
                other.balance += amount;
                
                addTransaction("Transferred: $" + to_string(amount) + " to account " + to_string(other.accountNumber));
                other.addTransaction("Received: $" + to_string(amount) + " from account " + to_string(accountNumber));
                
                cout << "Transferred $" << amount << " from account " 
                     << accountNumber << " to account " << other.accountNumber << endl;
            } else {
                cout << "Insufficient balance for transfer!" << endl;
            }
        } else {
            cout << "Invalid transfer amount!" << endl;
        }
    }

    // Calculate interest
    void calculateInterest(double rate) {
        double interest = balance * (rate / 100.0);
        balance += interest;
        addTransaction("Interest added: $" + to_string(interest) + " at " + to_string(rate) + "%");
        cout << "Interest of $" << interest << " added to account " << accountNumber << endl;
    }

    // Display transaction history
    void displayTransactionHistory() {
        cout << "\n--- Transaction History for Account " << accountNumber << " ---" << endl;
        cout << "Account Holder: " << name << endl;
        cout << "Current Balance: $" << balance << endl;
        cout << "\nRecent Transactions:" << endl;
        
        if (transactionCount == 0) {
            cout << "No transactions yet." << endl;
        } else {
            for (int i = 0; i < transactionCount; i++) {
                cout << (i + 1) << ". " << transactionHistory[i] << endl;
            }
        }
        cout << "-----------------------------------------------" << endl;
    }

    // Getters
    int getAccountNumber() { return accountNumber; }
    string getName() { return name; }
    double getBalance() { return balance; }
};

int main() {
    // Create accounts
    BankAccount acc1(1001, "Alice Johnson", 5000.0);
    BankAccount acc2(1002, "Bob Smith", 3000.0);
    BankAccount acc3(1003, "Charlie Brown", 10000.0);

    cout << "========== BANK SYSTEM INITIALIZED ==========" << endl;

    // Perform various operations
    cout << "\n========== DEPOSITS ==========" << endl;
    acc1.deposit(1500);
    acc2.deposit(500);

    cout << "\n========== WITHDRAWALS ==========" << endl;
    acc1.withdraw(2000);
    acc3.withdraw(3000);

    cout << "\n========== TRANSFERS ==========" << endl;
    acc1.transfer(acc2, 1000);
    acc3.transfer(acc1, 2500);

    cout << "\n========== INTEREST CALCULATION ==========" << endl;
    acc1.calculateInterest(5.0);  // 5% interest
    acc2.calculateInterest(5.0);
    acc3.calculateInterest(5.0);

    // More transactions
    cout << "\n========== MORE TRANSACTIONS ==========" << endl;
    acc2.deposit(750);
    acc2.transfer(acc3, 500);
    acc1.withdraw(1000);

    // Display transaction histories
    cout << "\n========== TRANSACTION HISTORIES ==========" << endl;
    acc1.displayTransactionHistory();
    acc2.displayTransactionHistory();
    acc3.displayTransactionHistory();

    // Display final balances
    cout << "\n========== FINAL BALANCES ==========" << endl;
    cout << "Account " << acc1.getAccountNumber() << " (" << acc1.getName() 
         << "): $" << acc1.getBalance() << endl;
    cout << "Account " << acc2.getAccountNumber() << " (" << acc2.getName() 
         << "): $" << acc2.getBalance() << endl;
    cout << "Account " << acc3.getAccountNumber() << " (" << acc3.getName() 
         << "): $" << acc3.getBalance() << endl;

    return 0;
}
```

</details>