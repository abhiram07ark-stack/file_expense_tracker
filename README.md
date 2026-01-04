# file_expense_tracker
Simple Expense Tracker in Python. Add, view, and calculate total expenses stored in a text file. Menu-driven interface for easy tracking of date, category, amount, and description. Stores data persistently in 'expense_tracker.txt'.
FILENAME=('expense_tracker.txt') 
# Defines the file name where expenses will be stored.

def add_expense(): 
# Defines a function to add a new expense.

    date=input("Enter the date") 
    # Takes date input from the user.

    category=input("Enter the category") 
    # Takes expense category input.

    amount=input("Enter the amount") 
    # Takes expense amount input.

    description=input("Enter comment") 
    # Takes a short description of the expense.

    with open(FILENAME,'a') as file: 
    # Opens the file in append mode; creates it if it doesn't exist.

        file.write(f'{date},{category},{amount},{description}\n') 
        # Writes the expense details as a comma-separated line.

        print("Expense added successfully") 
        # Confirms the expense was added.

def view_expenses(): 
# Defines a function to view all recorded expenses.

    try:
        with open(FILENAME,'r') as file: 
        # Opens the file in read mode.

            expenses=file.readlines() 
            # Reads all lines into a list.

            if not expenses: 
                print("No expenses recorded") 
                return 
            # Checks if the file is empty.

            print("\nDate\t\tCategory\tAmount\tDescription") 
            print("-" * 50) 
            # Prints header for the expenses table.

            for expense in expenses: 
                date,category,amount,description=expense.strip().split(",") 
                # Splits each line into variables after removing newline.

                print(f"{date}\t{category}\t{amount}\t{description}") 
                # Prints formatted expense details.

                print() 
                # Adds a blank line after each expense.

    except FileNotFoundError: 
        print("No Expenses to View") 
        # Handles case if file does not exist.

    except ValueError: 
        print("No values assigned yet") 
        # Handles case of incorrectly formatted data.

def total_expenses(): 
# Defines a function to calculate the total expense.

    total=0 
    # Initializes total expense variable.

    try:
        with open(FILENAME,'r') as file: 
        # Opens the file in read mode.

            for line in file: 
                data=line.strip().split(",") 
                # Splits each line into components.

                total+=float(data[2]) 
                # Adds the amount to total.

                print("Total expense",total) 
                # Prints total after adding each line.

    except FileNotFoundError: 
        print("No expenses entered yet") 
        # Handles case if file does not exist.

def menu(): 
# Defines the main menu function to interact with user.

    while True: 
        print("Expense Tracker") 
        print("1. Add Expense") 
        print("2. View Expenses") 
        print("3. Show Total Expenses") 
        print("4. Exit") 
        # Prints the menu options.

        choice=int(input("Enter your task")) 
        # Takes user input for menu selection.

        if choice==1: 
            add_expense() 
            # Calls function to add expense.

        elif choice==2: 
            view_expenses() 
            # Calls function to view expenses.

        elif choice==3: 
            total_expenses() 
            # Calls function to show total expenses.

        elif choice==4: 
            print("Exiting program") 
            break 
            # Exits the menu loop.

        else: 
            print("Invalid Input") 
            # Handles invalid menu selection.

menu() 
# Calls the menu function to start the program.
