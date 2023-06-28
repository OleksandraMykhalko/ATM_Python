# ATM_Python
Atm menu coding
class ATM:
    def __init__(self, balance, pin):
        self.balance = balance
        self.pin = pin

    def check_balance(self):
        return self.balance

    def deposit(self, amount):
        self.balance += amount
        return self.balance

    def withdraw(self, amount):
        if self.balance >= amount:
            self.balance -= amount
            return amount
        else:
            return "Insufficient funds."


def verify_pin(attempts=3):
    correct_pin = "1234"  # Replace with your desired PIN

    while attempts > 0:
        pin = input("Enter your PIN: ")
        if pin == correct_pin:
            print("PIN verification successful.")
            return True
        else:
            attempts -= 1
            print("Incorrect PIN. Attempts remaining:", attempts)
            if attempts > 0:
                print("Please try again.")

    print("PIN verification failed. Exiting.")
    return False


def display_withdrawal_submenu():
    print("Withdrawal Amounts:")
    print("1. $20")
    print("2. $40")
    print("3. $60")
    print("4. $80")
    print("5. $100")
    print("6. $200")
    print("7. Other Amount")
    print("8. Back to Main Menu")


def display_deposit_submenu():
    print("Deposit Menu:")
    print("1. Enter Amount")
    print("2. Return to Main Menu")


# Example usage:
if verify_pin():
    atm = ATM(1000, "1234")  # Initialize ATM with a starting balance of 1000 and PIN
    while True:
        print("ATM Menu:")
        print("1. Check Balance")
        print("2. Deposit")
        print("3. Withdraw")
        print("4. Exit")
        choice = input("Enter your choice (1-4): ")

        if choice == "1":
            print("Current Balance:", atm.check_balance())

        elif choice == "2":
            display_deposit_submenu()
            deposit_choice = input("Enter your choice (1-2): ")
            if deposit_choice == "1":
                amount = float(input("Enter the amount to deposit: "))
                new_balance = atm.deposit(amount)
                print("Deposit successful. New Balance:", new_balance)
            elif deposit_choice == "2":
                continue
            else:
                print("Invalid choice. Please try again.")

        elif choice == "3":
            display_withdrawal_submenu()
            withdrawal_choice = input("Enter your choice (1-8): ")

            if withdrawal_choice in ["1", "2", "3", "4", "5", "6"]:
                withdrawal_amounts = [20, 40, 60, 80, 100, 200]
                amount = withdrawal_amounts[int(withdrawal_choice) - 1]
                if atm.balance >= amount:
                    new_balance = atm.withdraw(amount)
                    print("Withdrawal successful. Amount withdrawn:", amount)
                    print("New Balance:", new_balance)
                else:
                    print("Insufficient funds.")

            elif withdrawal_choice == "7":
                custom_amount = int(input("Enter the withdrawal amount (must be a multiple of 10): "))
                if custom_amount % 10 == 0 and atm.balance >= custom_amount:
                    new_balance = atm.withdraw(custom_amount)
                    print("Withdrawal successful. Amount withdrawn:", custom_amount)
                    print("New Balance:", new_balance)
                else:
                    print("Invalid amount or insufficient funds.")

            elif withdrawal_choice == "8":
                continue

            else:
                print("Invalid choice. Please try again.")

        elif choice == "4":
            print("Thank you for using the ATM. Goodbye!")
            break

        else:
            print("Invalid choice. Please try again.")
