#include <iostream>
#include <string>
using namespace std;

class BankAccount {
private:
    string accountNumber;
    string holderName;
    double balance;

public:
    BankAccount(string accNumber, string name, double initialBalance)
        : accountNumber(accNumber), holderName(name), balance(initialBalance) {
        if (balance < 0) {
            cout << "Kesalahan: Saldo awal tidak boleh negatif. Saldo diatur menjadi 0.\n";
            balance = 0;
        }
    }

    void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            cout << "Berhasil menyetor Rp " << amount << ". Saldo baru: Rp " << balance << "\n";
        } else {
            cout << "Kesalahan: Jumlah setoran harus lebih dari 0.\n";
        }
    }

    void withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            cout << "Berhasil menarik Rp " << amount << ". Saldo baru: Rp " << balance << "\n";
        } else {
            cout << "Kesalahan: Penarikan gagal. Pastikan jumlah valid dan saldo cukup.\n";
        }
    }

    void transfer(BankAccount &recipient, double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            recipient.balance += amount;
            cout << "Berhasil mentransfer Rp " << amount << " ke " << recipient.holderName << ".\n";
            cout << "Saldo baru Anda: Rp " << balance << "\n";
        } else {
            cout << "Kesalahan: Transfer gagal. Pastikan jumlah valid dan saldo cukup.\n";
        }
    }

    void displayBalance() const {
        cout << "Akun: " << accountNumber << " | Pemilik: " << holderName << " | Saldo: Rp " << balance << "\n";
    }
};

int main() {
    BankAccount acc1("123456", "Alice", 500);
    BankAccount acc2("654321", "Bob", 300);

    acc1.displayBalance();
    acc2.displayBalance();

    acc1.deposit(200);
    acc1.withdraw(100);
    acc1.transfer(acc2, 250);
    
    acc1.displayBalance();
    acc2.displayBalance();

    return 0;
}
