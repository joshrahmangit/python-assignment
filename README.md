# python-assignment

# Menu dictionary
menu = {
    "Snacks": {
        "Cookie": .99,
        "Banana": .69,
        "Apple": .49,
        "Granola bar": 1.99
    },
    "Meals": {
        "Burrito": 4.49,
        "Teriyaki Chicken": 9.99,
        "Sushi": 7.49,
        "Pad Thai": 6.99,
        "Pizza": {
            "Cheese": 8.99,
            "Pepperoni": 10.99,
            "Vegetarian": 9.99
        },
        "Burger": {
            "Chicken": 7.49,
            "Beef": 8.49
        }
    },
    "Drinks": {
        "Soda": {
            "Small": 1.99,
            "Medium": 2.49,
            "Large": 2.99
        },
        "Tea": {
            "Green": 2.49,
            "Thai iced": 3.99,
            "Irish breakfast": 2.49
        },
        "Coffee": {
            "Espresso": 2.99,
            "Flat white": 2.99,
            "Iced": 3.49
        }
    },
    "Dessert": {
        "Chocolate lava cake": 10.99,
        "Cheesecake": {
            "New York": 4.99,
            "Strawberry": 6.49
        },
        "Australian Pavlova": 9.99,
        "Rice pudding": 4.99,
        "Fried banana": 4.49
    }
}

# Order list to store customer's selections
order = []

# Launch the store and present a greeting to the customer
print("Welcome to the variety food truck.")

# Customers may want to order multiple items, so let's create a continuous loop
place_order = True
while place_order:
    # Ask the customer from which menu category they want to order
    print("From which menu would you like to order? ")

    # Create a variable for the menu item number
    i = 1
    # Create a dictionary to store the menu for later retrieval
    menu_items = {}

    # Print the options to choose from menu headings (all the first level dictionary items in menu).
    for key in menu.keys():
        print(f"{i}: {key}")
        # Store the menu category associated with its menu item number
        menu_items[i] = key
        i += 1

    # Input validation for category selection
    category_choice = input("Please select a category by entering the number: ")

    if category_choice.isdigit():
        category_choice = int(category_choice)
        if category_choice in menu_items:
            # Retrieve the chosen category
            menu_category = menu_items[category_choice]
            print(f"You've selected {menu_category}. Here are the items:")
            
            # Display items in the selected category
            item_num = 1
            item_dict = {}
            for item, value in menu[menu_category].items():
                if isinstance(value, dict):
                    for sub_item, sub_price in value.items():
                        print(f"{item_num}. {item} ({sub_item}): ${sub_price}")
                        item_dict[item_num] = (item, sub_item, sub_price)
                        item_num += 1
                else:
                    print(f"{item_num}. {item}: ${value}")
                    item_dict[item_num] = (item, value)
                    item_num += 1

            # Ask the customer to choose an item
            item_choice = int(input("Select the item number: "))
            
            # First part of Step 4: check if the input is valid
            if item_choice in item_dict:
                # Retrieve item name and store it as a variable
                selected_item = item_dict[item_choice]
                if isinstance(selected_item, tuple) and len(selected_item) == 3:
                    item_name = f"{selected_item[0]} ({selected_item[1]})"
                    price = selected_item[2]
                else:
                    item_name = selected_item[0]
                    price = selected_item[1]

                # Ask for the quantity, and default to 1 if invalid
                quantity_input = input(f"How many {item_name} would you like? (default: 1 if invalid) ")
                
                # Validate the input and set quantity
                if not quantity_input.isdigit():
                    quantity = 1
                    print(f"Invalid input, setting quantity to 1.")
                else:
                    quantity = int(quantity_input)
                    print(f"Quantity set to {quantity}.")

                # Final part of Step 4: append the order to the order list
                order.append({
                    "Item name": item_name,
                    "Price": price,
                    "Quantity": quantity
                })
                print(f"Added {quantity} {item_name} to your order.")

            else:
                print("Invalid item selection.")
        else:
            print("Invalid category selection.")
    else:
        print("Please enter a valid number.")

    # Step 5: Ask the customer if they would like to keep ordering
    keep_ordering = input("Would you like to keep ordering? (Y)es or (N)o ").lower()

    # match:case statement for checking input and breaking the loop
    match keep_ordering:
        case 'y':
            place_order = True
            break  # Break from the loop and continue the ordering process
        case 'n':
            place_order = False
            print("Thank you for your order.")
            break  # Break from the loop and exit the ordering process
        case _:
            print("Invalid input, please try again.")

# Step 6: For loop to loop through the order list
print("
Your Order Summary:")
print("Item name                 | Price  | Quantity")
print("--------------------------|--------|----------")
for item in order:
    # Step 7: Saving values as separate variables
    item_name = item["Item name"]
    price = item["Price"]
    quantity = item["Quantity"]

    # Step 9: Create space strings using string multiplication
    item_name_spaces = ' ' * (26 - len(item_name))  # Fixed width for item name (26 characters)
    price_spaces = ' ' * (6 - len(f"${price:.2f}"))  # Fixed width for price (6 characters)

    # Step 10: Print the formatted receipt using the format from Step 8
    print(f"{item_name}{item_name_spaces}| ${price:.2f}{price_spaces}| {quantity}")

# Step 11: Calculate and display the total price
total_price = sum(item["Price"] * item["Quantity"] for item in order)
print(f"
Total Price: ${total_price:.2f}")

This code was created with assistance from ChatGpt

