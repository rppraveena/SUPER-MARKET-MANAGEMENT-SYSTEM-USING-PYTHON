# SUPER-MARKET-MANAGEMENT-SYSTEM-USING-PYTHON
class SupermarketManagementSystem:
    def __init__(self):
        self.inventory = {}
        self.sales_history = {}

    def add_product(self, product_id, product_name, quantity, price):
        self.inventory[product_id] = {'name': product_name, 'quantity': quantity, 'price': price}
        print(f"Product '{product_name}' with ID '{product_id}' added to inventory.")

    def remove_product(self, product_id):
        if product_id in self.inventory:
            product_name = self.inventory[product_id]['name']
            del self.inventory[product_id]
            print(f"Product '{product_name}' with ID '{product_id}' removed from inventory.")
        else:
            print("Product not found in inventory.")

    def update_quantity(self, product_id, new_quantity):
        if product_id in self.inventory:
            self.inventory[product_id]['quantity'] = new_quantity
            print("Quantity updated successfully.")
        else:
            print("Product not found in inventory.")

    def make_sale(self, product_id, quantity):
        if product_id in self.inventory:
            product_name = self.inventory[product_id]['name']
            price = self.inventory[product_id]['price']
            total = price * quantity
            if self.inventory[product_id]['quantity'] >= quantity:
                self.inventory[product_id]['quantity'] -= quantity
                self.sales_history.setdefault(product_id, {'quantity': 0, 'revenue': 0})
                self.sales_history[product_id]['quantity'] += quantity
                self.sales_history[product_id]['revenue'] += total
                print(f"Sale of '{quantity}' units of '{product_name}' completed. Total: ${total}")
            else:
                print(f"Not enough quantity of '{product_name}' in stock.")
        else:
            print("Product not found in inventory.")

    def display_inventory(self):
        print("Inventory:")
        for product_id, details in self.inventory.items():
            sold_quantity = self.sales_history.get(product_id, {'quantity': 0})['quantity']
            remaining_quantity = details['quantity'] - sold_quantity
            total_revenue = self.sales_history.get(product_id, {'revenue': 0})['revenue']
            print(f"ID: {product_id}, Name: {details['name']}, Current Quantity: {remaining_quantity}, Sold Quantity: {sold_quantity}, Price: ${details['price']}, Total Revenue: ${total_revenue}")


# Interface
def main():
    system = SupermarketManagementSystem()
    while True:
        print("\nWelcome to the Supermarket Management System")
        print("1. Add Product")
        print("2. Remove Product")
        print("3. Update Quantity")
        print("4. Make Sale")
        print("5. Display Inventory")
        print("6. Exit")

        choice = input("Enter your choice: ")

        if choice == '1':
            product_id = input("Enter product ID: ")
            product_name = input("Enter product name: ")
            quantity = int(input("Enter quantity: "))
            price = float(input("Enter price: "))
            system.add_product(product_id, product_name, quantity, price)

        elif choice == '2':
            product_id = input("Enter product ID to remove: ")
            system.remove_product(product_id)

        elif choice == '3':
            product_id = input("Enter product ID to update quantity: ")
            new_quantity = int(input("Enter new quantity: "))
            system.update_quantity(product_id, new_quantity)

        elif choice == '4':
            product_id = input("Enter product ID for sale: ")
            quantity = int(input("Enter quantity for sale: "))
            system.make_sale(product_id, quantity)

        elif choice == '5':
            system.display_inventory()

        elif choice == '6':
            print("Exiting Supermarket Management System. Goodbye!")
            break

        else:
            print("Invalid choice. Please try again.")


if __name__ == "__main__":
    main()

