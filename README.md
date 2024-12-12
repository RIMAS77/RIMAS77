import csv
def load_prices(filename):
    prices = {}
    with open(filename, 'r') as file:
        reader = csv.reader(file)
        for row in reader:
            prices[row[0]] = float(row[1])
    return prices


def process_order(pizza_size, toppings, pizza_prices, topping_prices):
    base_price = pizza_prices[pizza_size]

    topping_price = 0
    for topping in toppings:
        topping_price += topping_prices[topping]

    total_price = base_price + topping_price
    return total_price


def main():
    pizza_prices = load_prices('pizza_prices.csv')
    topping_prices = load_prices('topping_prices.csv')

    bank_balance = 1000.00

    while True:
        print("\nWelcome to the Pizza Shop!")
        print("1. Order Pizza")
        print("2. View Bank Balance")
        print("3. Exit")

        choice = input("Choose an option: ")

        if choice == '1':
            pizza_size = input("Choose pizza size (small, medium, large): ").lower()
            toppings_input = input("Enter toppings (comma-separated): ").lower()
            toppings = [topping.strip() for topping in toppings_input.split(',')]


            if pizza_size in pizza_prices and all(topping in topping_prices for topping in toppings):
                total_price = process_order(pizza_size, toppings, pizza_prices, topping_prices)
                bank_balance += total_price
                print(f"Your total price is ${total_price:.2f}")
            else:
                print("Invalid pizza size or topping(s), please try again.")


        elif choice == '2':
            print(f"Your current bank balance is ${bank_balance:.2f}")


        elif choice == '3':
            print("Thank you for visiting the Pizza Shop!")
            break


        else:
            print("Invalid option, please try again.")


if __name__ == "__main__":
    main()

