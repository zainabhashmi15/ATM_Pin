# ATM_Pin

MAX_ATTEMPTS = 3  # maximum number of incorrect PIN attempts
CORRECT_PIN = "1234"  # the correct PIN
AVAILABLE_BALANCE = 1000000  # the available balance in the account

def withdraw_amount(balance):
    """
    Prompts the user to enter an amount to withdraw and returns the updated balance after deducting the amount.

    balance: float, the current available balance in the account.
    returns: float, the updated balance after deducting the amount the user wants to withdraw.
    """
    while True:
        try:
            amount = float(input("Enter amount to withdraw: "))
            if amount > balance:
                print("Error: insufficient funds.")
            else:
                return balance - amount
        except ValueError:
            print("Error: invalid amount.")

# Main program loop
attempts = 0  # number of incorrect PIN attempts
while attempts < MAX_ATTEMPTS:
    pin = input("Enter your PIN: ")
    if pin == CORRECT_PIN:
        print("Welcome to the ATM!")
        balance = AVAILABLE_BALANCE
        while True:
            balance = withdraw_amount(balance)
            print(f"Current balance: ${balance:.2f}")
            response = input("Do you want to withdraw more cash? (y/n) ")
            if response.lower() != "y":
                print("Goodbye!")
                break
        break
    else:
        attempts += 1
        print(f"Incorrect PIN ({attempts}/{MAX_ATTEMPTS}).")
else:
    print("Your card is blocked.")
