
# Supermarket Billing System

A simple Python-based supermarket billing system that simulates a basic shopping experience in a supermarket. The system allows customers to add items to their cart, view a menu with item prices, and generate a detailed receipt with applied discounts based on the total amount. This project is implemented using Python, demonstrating fundamental programming concepts such as loops, functions, dictionaries, and input handling.

## Features

- **Menu Display:** Shows a list of available items and their prices.
- **Cart Management:** Allows customers to add multiple items to the cart, with quantities specified for each item.
- **Receipt Generation:** Prints a detailed receipt that includes item names, quantities, prices, subtotal, discount (if applicable), and the final total.
- **Discount Calculation:** Automatically applies a discount based on the total purchase amount:
  - 10% discount for purchases over 1000 INR.
  - 5% discount for purchases over 500 INR.
- **Modular Code Structure:** The code is organized into functions for better readability and maintenance.

## How to Run the Program

1. **Requirements:** Make sure you have Python installed on your system (Python 3.6 or higher is recommended).
2. **Run the Code:** Execute the code in a Python environment (e.g., Jupyter Notebook, VS Code, or directly from the command line).
3. **Follow the Prompts:** The program will prompt you to enter your name, phone number, and then add items to your cart. After adding items, you can print the receipt to see the final bill.

## Source Code

Below is the complete Python code for the supermarket billing system:

```python
# While True loop will help us to execute the billing for every new customer
while True:
    print("*"*48)
    text = "Welcome to the Super Market System"
    padded_text = text.center(48)
    print(padded_text)
    print("*"*48)

    # Below mentioned name and phone variable will take the input for customer name & phone number
    name = input("Enter Customer's Name:")
    phone = int(input("Enter Phone Number   :"))

    # Dictionary of menu items from the super market
    menu_items = {
            "Apple": 50.0,
            "Banana": 60.0,
            "Orange": 70.0,
            "Bread": 35.0,
            "Milk": 28.0,
            "Eggs": 60.0,
            "Rice": 80.0,
            "Pasta": 65.0,
            "Tomato": 35.0,
            "Onion": 22.0,
            "Potato": 30.0,
            "Butter": 75.0,
            "Cheese": 190.0,
            "Yogurt": 30.0,
            "Coffee": 210.0,
            "Tea": 90.0,
            "Chocolate": 110.0,
            "Cereal": 150.0,
            "Detergent": 180.0
        }
    
    # Displaying the Menu
    print("*"*48)
    print("Menu Items"," "*11,"Price(Rs.)")
    print("*"*48)
    for i,j in menu_items.items():
        print("{:<24}{:<24}".format(i,j))
    print("*"*48)

    # Initial Cart Setup
    amount = 0
    discount = 0
    final_amount = 0
    cart = {}

    # Here we used loop for adding Items to the Cart
    while True:
        flag = 0

        # Takes the input for the item name to add in cart
        item_name = input("Enter item name:").title()
        for item, cost in menu_items.items():
            if item_name == item:
                flag = 1
                break

        # Invallid item handling
        if flag == 0:
            print("Invalid item name")
            continue

        # Quantity and Cart Management
        # Asks for the item quantity and converts it to an integer.
        quantity = int(input("Enter no. of quantity:"))

        # Adds quantity to the dictionary
        if item_name in cart:
            cart[item_name] += quantity
        else:
            cart[item_name] = quantity 

        # Calculates initial amount
        amount += menu_items[item_name] * quantity

        #Asks if the user wants to add more items or print the receipt.
        #Repeats the prompt until a valid input (y or n) is given.
        while True:
            add_items = input("""Do you want to add more items? (y/n):""")

            if add_items not in ("y","n","Y","N"):
                print("Enter valid input")
            else:
                break
                
        #If n or N is entered, the program breaks out of the inner loop to proceed to receipt generation.
        if add_items == "n" or add_items == "N":
            print("\n")
            print("-"*18, "Receipt", "-"*18)
            print("Name:", name)
            print("Phone Number:", phone)
            print("-"*45)
             # Prints Headers (Item, Quantity, Price, Total)
            print("{:<15} {:<11} {:<9} {:<12}".format("Item", "Quantity", "Price", "Total"))
            print("-"*45)
            # Prints Items from the cart
            for x,y in cart.items():
                print("{:<15} {:<11} {:<9} {:<12}".format(x, y, menu_items[x], y * menu_items[x]))
            print("-"*45)
            #Prints the subtotal, which is the initial amount
            print("Subtotal     :", amount)

            # Calculates a discount based on the subtotal amount
            if amount >= 1000:
                discount += round(amount * 0.1, 2)  # Rounds off to 2 decimal places
                per = 10
            elif amount >= 500:
                discount += round(amount * 0.05, 2)  # Rounds off to 2 decimal places
                per = 5
            else:
                discount = 0
                per = 0
            print(f"Discount({per}%): -{discount}")

            #Calculates the final amount
            final_amount = amount - discount
            print("Total Amount :", final_amount)

            #End of Receipt
            print("-"*45)
            text2 = "THANK YOU FOR VISITING"
            padded_text2 = text2.center(45)
            print(padded_text2)
            text3 = "PLEASE COME AGAIN"
            padded_text3 = text3.center(45)
            print(padded_text3)
            print("-"*45)
            print("\n\n")
            break
```

## Example Output

```
************************************************
       Welcome to the Super Market System       
************************************************
Enter Customer's Name: Manik Gupta
Enter Phone Number   : 9149525858
************************************************
Menu Items             Price(Rs.)
************************************************
Apple                   50.0                    
Banana                  60.0                    
Orange                  70.0                    
Bread                   35.0                    
...              
************************************************
Enter item name: Cereal
Enter no. of quantity: 4
Do you want to add more items? (y/n): y
Enter item name: Coffee
Enter no. of quantity: 5
Do you want to add more items? (y/n): n

------------------ Receipt ------------------
Name: Manik Gupta
Phone Number: 1234567890
---------------------------------------------
Item            Quantity    Price     Total       
---------------------------------------------
Cereal          4           150.0     600.0       
Coffee          5           210.0     1050.0      
---------------------------------------------
Subtotal     : 1650.0
Discount(10%): -165.0
Total Amount : 1485.0
---------------------------------------------
            THANK YOU FOR VISITING           
              PLEASE COME AGAIN              
---------------------------------------------
```
## License

This project is open-source and available under the MIT License.
