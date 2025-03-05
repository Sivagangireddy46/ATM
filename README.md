class ATM:
    def __init__(self):
        self.accounts = {"Sivagangireddy46": {"pin": "1234", "balance": 1000}}

    def check_balance(self, username):
        return self.accounts[username]["balance"]

    def deposit(self, username, amount):
        self.accounts[username]["balance"] += amount
        return self.accounts[username]["balance"]

    def withdraw(self, username, amount):
        if self.accounts[username]["balance"] >= amount:
            self.accounts[username]["balance"] -= amount
            return self.accounts[username]["balance"]
        else:
            return "Insufficient funds"

    def authenticate(self, username, pin):
        if username in self.accounts and self.accounts[username]["pin"] == pin:
            return True
        return False

def main():
    atm = ATM()
    print("Welcome to the ATM")
    username = input("Enter your username: ")
    pin = input("Enter your PIN: ")

    if atm.authenticate(username, pin):
        print("Login successful!")
        while True:
            print("\n1. Check Balance")
            print("\n2. Deposit Money")
            print("\n3. Withdraw Money")
            print("\n4. Exit")
            choice = input("Choose an option: ")

            if choice == "1":
                balance = atm.check_balance(username)
                print(f"Your balance is: ${balance}")
            elif choice == "2":
                amount = float(input("Enter amount to deposit: "))
                new_balance = atm.deposit(username, amount)
                print(f"Deposit successful! New balance: ${new_balance}")
            elif choice == "3":
                amount = float(input("Enter amount to withdraw: "))
                result = atm.withdraw(username, amount)
                if result == "Insufficient funds":
                    print(result)
                else:
                    print(f"Withdrawal successful! New balance: ${result}")
            elif choice == "4":
                print("Thank you for using the ATM. Goodbye!")
                break
            else:
                print("Invalid option. Please try again.")
    else:
        print("Authentication failed. Incorrect username or PIN.")

if __name__ == "__main__":
    main()
