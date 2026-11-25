# GST Calculator Using Python Operators

VALID_SLABS = [0, 5, 12, 18, 28]  # Common GST slabs in India (%)


def get_non_negative_number(prompt):
    """Prompt until a valid non-negative number is entered."""
    while True:
        raw_value = input(prompt).strip()
        try:
            amount = float(raw_value)
        except ValueError:
            print("Invalid input. Please enter a numeric value.")
            continue

        # Comparison (>=) and logical (and) operators
        if amount >= 0 and amount == amount:
            return amount

        print("Amount cannot be negative. Try again.")


def get_gst_rate():
    """Prompt until a valid GST slab is selected."""
    while True:
        rate = get_non_negative_number(f"Enter GST slab {VALID_SLABS}: ")

        # Membership operator (in)
        if rate in VALID_SLABS:
            return rate

        print("Slab not in allowed list. Please choose a valid slab.")


def calculate_add_gst(base_price, rate):
    """Calculate GST and final price from a base price."""
    # Arithmetic operators (*, /, +)
    gst_amount = (base_price * rate) / 100
    final_price = base_price + gst_amount
    return base_price, gst_amount, final_price


def calculate_remove_gst(inclusive_price, rate):
    """Extract base price and GST from a GST-inclusive amount."""
    # Arithmetic operators (*, /, +, -)
    base_price = (inclusive_price * 100) / (100 + rate)
    gst_amount = inclusive_price - base_price
    return base_price, gst_amount, inclusive_price


def print_summary(base_price, gst_amount, final_price, rate):
    """Display itemized bill with equal CGST and SGST split."""
    # Arithmetic operator (/)
    cgst = gst_amount / 2
    sgst = gst_amount / 2

    print("\n" + "=" * 36)
    print(f"{'Base Price':<18}: Rs. {base_price:>10.2f}")
    print(f"{'CGST (' + str(rate / 2) + '%)':<18}: Rs. {cgst:>10.2f}")
    print(f"{'SGST (' + str(rate / 2) + '%)':<18}: Rs. {sgst:>10.2f}")
    print(f"{'Total GST':<18}: Rs. {gst_amount:>10.2f}")
    print(f"{'Final Total':<18}: Rs. {final_price:>10.2f}")
    print("=" * 36)


def main():
    print("=== GST Calculator (Python Operators) ===")

    # Assignment operators (=)
    running_total = 0.0
    transaction_count = 0

    while True:
        print("\nSelect an option:")
        print("1. Add GST to base price")
        print("2. Remove GST from inclusive price")
        print("3. Exit")

        choice = input("Enter choice (1/2/3): ").strip()

        # Identity / equality comparison (==)
        if choice == "1":
            base_price = get_non_negative_number("Enter base price: ")
            rate = get_gst_rate()
            base, gst, total = calculate_add_gst(base_price, rate)
            print_summary(base, gst, total, rate)

            # Assignment operators (+=)
            running_total += total
            transaction_count += 1

        elif choice == "2":
            inclusive_price = get_non_negative_number("Enter GST-inclusive price: ")
            rate = get_gst_rate()
            base, gst, total = calculate_remove_gst(inclusive_price, rate)
            print_summary(base, gst, total, rate)

            running_total += total
            transaction_count += 1

        elif choice == "3":
            break

        else:
            print("Invalid choice. Enter 1, 2, or 3.")

    # Comparison operator (>)
    if transaction_count > 0:
        print(f"\nTotal calculations: {transaction_count}")
        print(f"Combined final amount: Rs. {running_total:.2f}")

    print("Exiting GST Calculator. Goodbye!")


if __name__ == "__main__":
    main()
