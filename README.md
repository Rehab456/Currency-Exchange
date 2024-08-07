def load_exchange_rates():
    file_contents = """AED:75.72
SAR:74.09
GBP:353.56
JPY:1.90
USD:278.13"""
    
    rates = {}
    for line in file_contents.strip().split('\n'):
        currency, rate = line.strip().split(':')
        rates[currency] = float(rate)
    return rates

def convert_to_pkr(amount, rate):
    return amount * rate

def convert_from_pkr(amount, rate):
    return amount / rate

def main():
    exchange_rates = load_exchange_rates()
    
    print("\nCurrency Converter")
    print("-" * 40)
    print("1: AED")
    print("2: SAR")
    print("3: GBP")
    print("4: JPY")
    print("5: USD")
    
    currency_options = {1: 'AED', 2: 'SAR', 3: 'GBP', 4: 'JPY', 5: 'USD'}

    while True:
        try:
            choice = int(input("Choose currency (1-5) or 0 to quit: "))
            if choice == 0:
                print("Goodbye!")
                break
            if choice in currency_options:
                currency = currency_options[choice]
                while True:
                    direction = input("Convert (1) from PKR to currency or (2) from currency to PKR? (or 0 to stop): ")
                    if direction == '0':
                        break
                    try:
                        amount = float(input(f"Enter amount (or 0 to stop): "))
                        if amount == 0:
                            break
                        rate = exchange_rates[currency]
                        if direction == '1':
                            converted_amount = convert_from_pkr(amount, rate)
                            print(f"{amount} PKR = {converted_amount:.2f} {currency}\n")
                        elif direction == '2':
                            converted_amount = convert_to_pkr(amount, rate)
                            print(f"{amount} {currency} = {converted_amount:.2f} PKR\n")
                        else:
                            print("Invalid direction, please enter 1 or 2.")
                    except ValueError:
                        print("Invalid amount, please try again.")
            else:
                print("Invalid choice, try again.")
        except ValueError:
            print("Invalid input, please enter a number.")

if __name__ == "__main__":
    main()
