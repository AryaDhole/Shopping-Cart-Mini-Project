# Shopping-Cart-Mini-Project
### Arya Dhole  ENTC-A2  22070123027

This program creates a shopping system that allows users to select products, add them to a cart, calculate the total cost, apply discounts based on the quantity purchased, and display the final bill and cart contents.
### Header :
```cpp
#include <iostream>
#include <string>
using namespace std;
```
These lines include the necessary C++ libraries for input/output and string manipulation.

### Constants :
```cpp
const int MAX_DEVICES = 20;
```
This constant defines the maximum number of devices (products) that can be stored in the shopping system.

### `Products` Class:
This class represents individual products and contains information about each product.

```cpp
class Products {
    public:
        string name;
        float price;
        int quantity;

        // Default constructor
        Products() : name(""), price(0), quantity(0) {}

        // Constructor with parameters to initialize name and price
        Products(const string& n, float p) : name(n), price(p), quantity(0) {}

        // Method to calculate the total price of a product
        float getTotalPrice() const {
            return price * quantity;
        }
};
```

- The `Products` class has three member variables: `name` (the name of the product), `price` (the price of the product), and `quantity` (the quantity of the product in the cart).
- It provides two constructors: a default constructor that initializes a product with empty name, zero price, and zero quantity, and a parameterized constructor that sets the name and price while initializing the quantity to zero.
- The `getTotalPrice()` method calculates and returns the total price of a product, which is the product's price multiplied by its quantity. It's marked as `const` because it doesn't modify the object's state.

### `ShoppingSystem` Class:
This class represents the shopping system and manages the available products and the shopping cart.

```cpp
class ShoppingSystem {
    public:
        Products devices[MAX_DEVICES];  // An array to store available devices
        int Item;  // Number of available devices
        int discountThreshold;  // Quantity threshold for discount
        int discountThreshold1;  // Second quantity threshold for discount
        float baseDiscountRate;  // Base discount rate
        float DiscountRate1;  // Discount rate for higher quantity

        // Constructor to initialize the product list and other attributes
        ShoppingSystem() : Item(0), discountThreshold(2), discountThreshold1(4), baseDiscountRate(0.05), DiscountRate1(0.1) {
            // Prepopulating the list of available products with their names and prices
            devices[Item++] = Products("iPhone 15", 80000);
            devices[Item++] = Products("iPhone 15 Pro", 120000);
            devices[Item++] = Products("Samsung S23", 85000);
            devices[Item++] = Products("Samsung S23 Plus", 95000);
            devices[Item++] = Products("Google Pixel 8", 75000);
            devices[Item++] = Products("Google Pixel 8 Pro", 95000);
     
            devices[Item++] = Products("Samsung Z Fold 6", 180000);
            devices[Item++] = Products("Samsung Z Flip 6", 100000);
            devices[Item++] = Products("OnePlus Open ", 135000);
            devices[Item++] = Products("Google Pixel Fold", 150000);
        
            devices[Item++] = Products("AirPods", 10000);
            devices[Item++] = Products("AirPods Pro", 15000);
            devices[Item++] = Products("Samsung Buds", 8500);
            devices[Item++] = Products("Samsung Buds Pro", 14000);
            devices[Item++] = Products("Pixel Buds", 8000);
            devices[Item++] = Products("Pixel Buds Plus", 13500);
        
            devices[Item++] = Products("Apple Watch Series 8", 55000);
            devices[Item++] = Products("Apple Watch Ultra", 85000);
            devices[Item++] = Products("Galaxy Watch 4", 35000);
            devices[Item++] = Products("Pixel Watch 2", 45000);
        }

        // Method to display the product menu
        void displayMenu();
        // Method to add a product to the cart
        void purchaseDevice(int choice, int quantity);
        // Method to calculate the total price of items in the cart
        float calculateTotalPrice();
        // Method to calculate applicable discounts
        float calculateDiscount();
};
```

- The `ShoppingSystem` class includes an array named `devices` to store available products and various attributes for managing discounts.
- The constructor initializes the list of available products and sets default values for discount-related attributes.
- It also includes several methods:
  - `displayMenu()`: Displays the product menu, categorized into "Smartphones," "Foldables," "Headphones," and "Smart Watches."
  - `purchaseDevice()`: Allows users to add products to their cart by specifying the product choice and quantity.
  - `calculateTotalPrice()`: Calculates the total bill for all the products in the cart.
  - `calculateDiscount()`: Calculates applicable discounts based on the total quantity of items in the cart and predefined thresholds.

### `main` Function:
The `main` function is the entry point of the program and controls the overall shopping experience.

```cpp
int main() {
    ShoppingSystem shoppingSystem;  // Create an instance of the ShoppingSystem class
    char choice;
    
    do {
        shoppingSystem.displayMenu();  // Display the product menu

        int deviceChoice;
        int quantity;

        cout << "Enter the number of the device you want to purchase (or 0 to finish): ";
        cin >> deviceChoice;

        if (deviceChoice == 0) {
            break;  // Exit the loop and finish shopping
        }

        if (deviceChoice < 0 || deviceChoice > MAX_DEVICES) {
            cout << "Invalid choice. Please try again." << endl;
            continue;  // Continue shopping if the choice is invalid
        }

        cout << "Enter the quantity: ";
        cin >> quantity;

        shoppingSystem.purchaseDevice(deviceChoice, quantity);  // Add the chosen product to the cart

        cout << "Do you want to continue shopping? (Y/N): ";
        cin >> choice;
    } while (choice == 'y' || choice == 'Y');  // Continue shopping if the user wants to

    // Calculate the total bill, discount, and final bill
    double totalBill = shoppingSystem.calculateTotalPrice();
    double discount = shoppingSystem.calculateDiscount();
    double finalBill = totalBill - discount;

    // Display the cart contents and the final bill
    cout << "-------------------------------" << endl;
    cout << "Cart Contents:" << endl;
    for (int i = 0; i < shoppingSystem.Item; ++i) {
        if (shoppingSystem.devices[i].quantity > 0) {
            cout << shoppingSystem.devices[i].name << " - Quantity: " << shoppingSystem.devices[i].quantity << endl;
        }
    }
    
    cout << "Total Bill Amount: " << totalBill << " INR" << endl;
    cout << "Discount Applied: " << discount << " INR" << endl;
    cout << "Final Bill Amount: " << finalBill << " INR" << endl;

    return 0;  // Exit the program
}
```

- The `main` function creates an instance of the `ShoppingSystem` class called `shoppingSystem`.
- It uses a loop to allow the user to interact with the shopping system.
- Inside the loop, it displays the product menu, allows the user to add products to their cart, and provides feedback on the purchases.
- The loop continues until the user chooses to finish shopping.
- After exiting the loop, it calculates the total bill, any applicable discounts, and the final bill.
- Finally, it displays the cart contents, total bill, applied discount, and final bill.

## Output:

```plaintext
Product Menu:

Smartphones

1. iPhone 15 - 80000 INR
2. iPhone 15 Pro - 120000 INR
3. Samsung S23 - 85000 INR
4. Samsung S23 Plus - 95000 INR
5. Google Pixel 8 - 75000 INR
6. Google Pixel 8 Pro - 95000 INR

Foldables

7. Samsung Z Fold 6 - 180000 INR
8. Samsung Z Flip 6 - 100000 INR
9. OnePlus Open  - 135000 INR
10. Google Pixel Fold - 150000 INR

Headphones

11. AirPods - 10000 INR
12. AirPods Pro - 15000 INR
13. Samsung Buds - 8500 INR
14. Samsung Buds Pro - 14000 INR
15. Pixel Buds - 8000 INR
16. Pixel Buds Plus - 13500 INR

Smart Watches

17. Apple Watch Series 8 - 55000 INR
18. Apple Watch Ultra - 85000 INR
19. Galaxy Watch 4 - 35000 INR
20. Pixel Watch 2 - 45000 INR

0. Checkout
-------------------------------
Enter the number of the device you want to purchase (or 0 to finish): 1
Enter the quantity: 2
2 iPhone 15 added to the cart.
Do you want to continue shopping? (Y/N): Y

Enter the number of the device you want to purchase (or 0 to finish): 9
Enter the quantity: 1
1 OnePlus Open added to the cart.
Do you want to continue shopping? (Y/N): Y

Enter the number of the device you want to purchase (or 0 to finish): 4
Enter the quantity: 1
1 Samsung S23 Plus added to the cart.
Do you want to continue shopping? (Y/N): Y

Enter the number of the device you want to purchase (or 0 to finish): 15
Enter the quantity: 1
1 Pixel Buds added to the cart.
Do you want to continue shopping? (Y/N): N
-------------------------------
Cart Contents:

iPhone 15 - Quantity: 2
OnePlus Open - Quantity: 1
Samsung S23 Plus - Quantity: 1
Pixel Buds - Quantity: 1

Total Bill Amount: 398000 INR
Discount Applied: 39800 INR
Final Bill Amount: 358200 INR
```

