#include <iostream>
#include <vector>
#include <string>

class Product {
public:
    int id;
    std::string name;
    double price;
    int stock;

    Product(int id, std::string name, double price, int stock)
        : id(id), name(name), price(price), stock(stock) {}

    void display() const {
        std::cout << "ID: " << id << " | Name: " << name << " | Price: $" << price 
                  << " | Stock: " << stock << std::endl;
    }

    bool isAvailable(int quantity) const {
        return stock >= quantity;
    }

    void reduceStock(int quantity) {
        stock -= quantity;
    }
};

class Customer {
public:
    int id;
    std::string name;

    Customer(int id, std::string name) 
        : id(id), name(name) {}

    void display() const {
        std::cout << "Customer ID: " << id << " | Name: " << name << std::endl;
    }
};

class Order {
public:
    int orderId;
    Customer customer;
    std::vector<Product> products;
    double total;

    Order(int orderId, Customer customer) 
        : orderId(orderId), customer(customer), total(0) {}

    void addProduct(const Product& product, int quantity) {
        products.push_back(product);
        total += product.price * quantity;
    }

    void displayOrder() const {
        std::cout << "\nOrder ID: " << orderId << " | Customer: " << customer.name 
                  << " | Total: $" << total << std::endl;
        for (const auto& product : products) {
            product.display();
        }
    }
};

int main() {
    std::vector<Product> products;
    int choice;
    int productIdCounter = 1;

    std::cout << "Welcome to the E-commerce Platform!\n";
    
    while (true) {
        std::cout << "\n1. Add Product to Inventory\n"
                  << "2. Search and Order Product\n"
                  << "3. Exit\n"
                  << "Enter your choice: ";
        std::cin >> choice;
        std::cin.ignore(); // Ignore newline left in the buffer

        if (choice == 1) {
            // Add product to inventory
            std::string name;
            double price;
            int stock;

            std::cout << "Enter product name: ";
            std::getline(std::cin, name);
            std::cout << "Enter product price: ";
            std::cin >> price;
            std::cout << "Enter product stock: ";
            std::cin >> stock;
            std::cin.ignore();

            products.push_back(Product(productIdCounter++, name, price, stock));
            std::cout << "Product added to inventory.\n";

        } else if (choice == 2) {
            // Search and order product
            std::string productName;
            int quantity;
            bool found = false;

            Customer customer(1, "John Doe");
            Order order(1, customer);

            std::cout << "Enter product name to search for: ";
            std::getline(std::cin, productName);

            for (auto& product : products) {
                if (product.name == productName) {
                    found = true;
                    product.display();

                    std::cout << "Enter quantity: ";
                    std::cin >> quantity;
                    std::cin.ignore();

                    if (product.isAvailable(quantity)) {
                        order.addProduct(product, quantity);
                        product.reduceStock(quantity);
                        std::cout << "Product added to order.\n";
                    } else {
                        std::cout << "Insufficient stock. Available quantity: " << product.stock << std::endl;
                    }
                    break;
                }
            }

            if (!found) {
                std::cout << "Product not found.\n";
            } else {
                std::cout << "\nOrder Summary:";
                order.displayOrder();
            }

        } else if (choice == 3) {
            std::cout << "Thank you for using the platform! Exiting.\n";
            break;
        } else {
            std::cout << "Invalid choice, please try again.\n";
        }
    }

    return 0;
}
