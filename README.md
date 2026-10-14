# Super Market Billing System

## About the Project

The Super Market Billing System is a Python project developed in Jupyter Notebook to manage basic supermarket billing operations. It allows customers to select products, enter quantities, calculate item-wise amounts, apply discounts, and generate a final itemized bill.

This project demonstrates the practical use of Python fundamentals, including dictionaries, tuples, lists, loops, conditional statements, exception handling, and formatted output.

## Features

- Displays a product catalogue with product ID, name, category, and price.
- Allows multiple products to be added to a single transaction.
- Accepts product IDs and quantities through interactive input.
- Calculates the amount for each selected product.
- Calculates the subtotal of all purchased items.
- Provides three discount options: no discount, flat discount, and percentage discount.
- Validates product IDs, quantities, discount choices, and discount amounts.
- Generates an itemized bill and final payment summary.

## Technologies Used

- Python
- Jupyter Notebook

## Project Structure

```text
super-market-billing-system/
│
├── Super_market_billing.ipynb
├── README.md
└── screenshots/
    └── billing-output.png
```

The screenshot filename above is a suggested name. Replace it with your actual filename if it differs.

## How to Run the Project

1. Clone or download this repository.
2. Install Python and Jupyter Notebook if they are not already installed.
3. Open the project notebook in Jupyter Notebook or JupyterLab.
4. Run the code cell.
5. Enter the product ID and quantity when prompted.
6. Choose whether to add more products.
7. Select a discount option and provide the requested value.
8. View the final itemized bill and payment summary.

## Python Source Code

The following code is taken from the project notebook.

```python
# ============================================================
#                 GROCERY BILLING SYSTEM
# ============================================================

# ---------------- PRODUCT LIST ----------------

print("=" * 90)
print("                         AVAILABLE PRODUCTS")
print("=" * 90)

print(f"{'Product':<25} {'Product ID':<15} "
      f"{'Category':<18} {'Price':>10}")
print("-" * 90)

# Dictionary containing all products
# Each product is stored as a tuple:
# (Product Name, Category, Price)

products = {
    1: ("Rice(1KG)", "Grocery", 60),
    2: ("Wheat flour(1KG)", "Grocery", 40),
    3: ("Milk(1L)", "Dairy", 60),
    4: ("Butter(100G)", "Dairy", 50),
    5: ("Cold Drink(500ml)", "Beverages", 40),
    6: ("Chips(40G)", "Snacks", 20),
    7: ("Biscuits(200G)", "Snacks", 30),
    8: ("Soap(125G)", "Personal_Care", 30),
    9: ("Shampoo(250ml)", "Personal_Care", 120),
    10: ("Detergent_Powder(1KG)", "HouseHold", 120)
}

# Display available products
for product_id, product_details in products.items():
    product_name, category, price = product_details

    print(f"{product_name:<25} "
          f"{'product_Id(' + str(product_id) + ')':<15} "
          f"{category:<18} {price:>10}")

print("=" * 90)

# ---------------- SHOPPING / BILLING ----------------

print("                              ITEMIZED BILL")
print("=" * 90)

print(f"{'Product':<25} {'Product ID':<15} "
      f"{'Qty':<10} {'Amount':>12}")
print("-" * 90)

# Empty list to store purchased products
cart = []

# ---------------- PRODUCT SELECTION ----------------

while True:
    try:
        product_id = int(input("Enter the product ID: "))

        # Check whether product ID exists
        if product_id not in products:
            print("Invalid Product ID! Please enter a valid product ID.")
            continue

        qty = int(input("Enter the quantity: "))

        # Validate quantity
        if qty <= 0:
            print("Quantity must be greater than 0.")
            continue

        # Get product information
        product_name, category, price = products[product_id]

        # Calculate item amount
        amount = price * qty

        # Store purchased item as a tuple
        item = (product_name, product_id, qty, price, amount)

        # Add item to cart
        cart.append(item)

        print(f"{product_name} x {qty} added successfully.")
        print(f"Amount: ₹{amount}")

        # Ask whether to add another product
        user = input("Do you want to add more products? (y/n): ")

        if user.lower() in ["n", "no"]:
            break

    except ValueError:
        print("Please enter numbers only.")

# ---------------- FINAL ITEMIZED BILL ----------------

print()
print("=" * 90)
print("                              FINAL BILL")
print("=" * 90)

print(f"{'Product':<25} {'Product ID':<15} "
      f"{'Qty':<10} {'Amount':>12}")
print("-" * 90)

# Calculate subtotal
subtotal = 0

for item in cart:
    product_name, product_id, qty, price, amount = item

    print(f"{product_name:<25} {product_id:<15} "
          f"{qty:<10} ₹{amount:>10}")

    subtotal = subtotal + amount

print("-" * 90)
print(f"{'SUBTOTAL':<65} ₹{subtotal:>10}")

# ---------------- DISCOUNT OPTIONS ----------------

print()
print("=" * 90)
print("                         DISCOUNT OPTIONS")
print("=" * 90)

print("1. No Discount")
print("2. Flat Discount")
print("3. Percentage Discount")
print("-" * 90)

while True:
    try:
        discount_type = int(
            input("Enter your discount choice (1/2/3): ")
        )

        if discount_type not in [1, 2, 3]:
            print("Please select 1, 2 or 3.")
            continue

        break

    except ValueError:
        print("Please enter 1, 2 or 3.")

# Default discount
discount = 0

# ---------------- NO DISCOUNT ----------------

if discount_type == 1:
    discount = 0
    print("No discount applied.")

# ---------------- FLAT DISCOUNT ----------------

elif discount_type == 2:
    while True:
        try:
            flat_discount = float(
                input("Enter flat discount amount: ₹")
            )

            if flat_discount < 0:
                print("Discount cannot be negative.")
                continue

            if flat_discount > subtotal:
                print("Discount cannot be greater than the subtotal.")
                continue

            discount = flat_discount
            break

        except ValueError:
            print("Please enter a valid amount.")

# ---------------- PERCENTAGE DISCOUNT ----------------

elif discount_type == 3:
    while True:
        try:
            discount_percentage = float(
                input("Enter discount percentage: ")
            )

            if discount_percentage < 0 or discount_percentage > 100:
                print("Percentage must be between 0 and 100.")
                continue

            # Calculate percentage discount
            discount = subtotal * discount_percentage / 100
            break

        except ValueError:
            print("Please enter a valid percentage.")

# ---------------- FINAL CALCULATION ----------------

final_amount = subtotal - discount

print()
print("=" * 90)
print("                         PAYMENT SUMMARY")
print("=" * 90)

print(f"{'Subtotal':<65} ₹{subtotal:>10}")
print(f"{'Discount':<65} ₹{discount:>10}")
print(f"{'Final Amount':<65} ₹{final_amount:>10}")

print("=" * 90)
print("                    THANK YOU FOR SHOPPING!")
print("=" * 90)
```

## Sample Output

The following example uses the same values as the saved notebook output.

**Products selected:**

| Product | Product ID | Quantity | Amount |
|---|---:|---:|---:|
| Rice (1KG) | 1 | 3 | ₹180 |
| Butter (100G) | 4 | 6 | ₹300 |
| **Subtotal** | | | **₹480** |

**Payment summary:**

| Description | Amount |
|---|---:|
| Subtotal | ₹480 |
| Flat discount | ₹100 |
| **Final amount** | **₹380** |

## Python Concepts Demonstrated

- **Dictionary:** Stores product details using product IDs.
- **Tuples:** Groups product information and purchased item details.
- **Lists:** Stores selected products in the shopping cart.
- **For loop:** Displays products and calculates the subtotal.
- **While loop:** Repeats product selection and validates user input.
- **Conditional statements:** Handle discount choices and validation.
- **Exception handling:** Handles invalid numeric input using `try` and `except`.
- **F-strings:** Format the product table and billing receipt.

## Learning Outcome

This project helped me practise Python programming fundamentals by applying them to a practical billing scenario. It strengthened my understanding of data structures, loops, conditional logic, input validation, calculations, and formatted output.

## Project Link

[View Super Market Billing System on GitHub](https://github.com/bs391095/super-market-billing-system)
