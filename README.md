def check_sack(contents, weight):
    """Checks the contents and weight of a single sack and returns a message."""
    if contents not in ["C", "G", "S"]:
        return "Invalid contents. Sack must contain cement (C), gravel (G), or sand (S)."

    if contents in ["G", "S"]:
        if not 49.9 <= weight <= 50.1:
            return "Incorrect weight for sand or gravel. Must be between 49.9 and 50.1 kg."
    else:
        if not 24.9 <= weight <= 25.1:
            return "Incorrect weight for cement. Must be between 24.9 and 25.1 kg."

    return f"Contents: {contents}, Weight: {weight:.1f} kg - Accepted"

def check_order():
    """Checks a customer's order for delivery, calculates price, and outputs details."""
    cement_sacks = int(input("Enter the number of cement sacks: "))
    gravel_sacks = int(input("Enter the number of gravel sacks: "))
    sand_sacks = int(input("Enter the number of sand sacks: "))

    accepted_sacks = 0
    total_weight = 0
    rejected_sacks = 0
    regular_price = 0
    for _ in range(cement_sacks):
        contents = input("Enter contents for cement sack (C): ").upper()
        weight = float(input("Enter weight for cement sack: "))
        message = check_sack(contents, weight)
        print(message)
        if "Accepted" in message:
            accepted_sacks += 1
            total_weight += weight
            regular_price += 3
        else:
            rejected_sacks += 1
    for _ in range(gravel_sacks):
        contents = input("\nEnter contents for gravel sack (G): ").upper()
        weight = float(input("\nEnter weight for gravel sack: "))
        message = check_sack(contents, weight)
        print(message)
        if "Accepted" in message:
            accepted_sacks += 1
            total_weight += weight
            regular_price += 2
        else:
            rejected_sacks += 1
    for _ in range(sand_sacks):
        contents = input("\nEnter contents for sand sack (S): ").upper()
        weight = float(input("\nEnter weight for sand sack: "))
        message = check_sack(contents, weight)
        print(message)
        if "Accepted" in message:
            accepted_sacks += 1
            total_weight += weight
            regular_price += 2
        else:
            rejected_sacks += 1
    print("\nTotal weight of accepted sacks:", total_weight, "kg")
    print("Number of sacks rejected:", rejected_sacks)
    print("Regular price: $", regular_price)
    special_packs = min(cement_sacks, gravel_sacks // 2, sand_sacks // 2)
    if special_packs > 0:
        discounted_price = regular_price - special_packs * 5
        amount_saved = special_packs * 5
        print("Discount price (", special_packs, "special pack(s)): $", discounted_price)
        print("Amount saved: $", amount_saved)
    else:
        print("No discount applicable.")

if __name__ == "__main__":
    check_order()
