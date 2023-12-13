# Author: [Tavar Motheraill]
# Date Created: [12/12/23]
# Course: ITT103
# Purpose: Automated reservation system for UCC Signature Express Limited

# Constants for seat capacities
FIRST_CLASS_CAPACITY = 27
BUSINESS_CLASS_CAPACITY = 38
ECONOMY_CLASS_CAPACITY = 56

# Initialize seat availability matrix
seats = [[''] * 2 for _ in range(FIRST_CLASS_CAPACITY + BUSINESS_CLASS_CAPACITY + ECONOMY_CLASS_CAPACITY)]

def display_menu():
    print("UCC Signature Express Limited")
    print("<Insert Your Own Tagline>")
    print("Reservation Options:")
    print("  F - First Class")
    print("  B - Business Class")
    print("  E - Economy Class")
    print("  Q - Quit or Cancel")

def reserve_seat(class_name):
    while True:
        try:
            row = int(input("Enter the row number (1 to {}): ".format(FIRST_CLASS_CAPACITY + BUSINESS_CLASS_CAPACITY + ECONOMY_CLASS_CAPACITY)))
            if row <= 0:
                print("Number must be positive or greater than zero!")
                continue

            column = int(input("Enter the column number (1 for window, 2 for aisle): "))
            if column not in (1, 2):
                print("Invalid column number. Please choose 1 for window or 2 for aisle.")
                continue

            if seats[row - 1][column - 1]:
                print("Seat already reserved. Please choose another seat.")
            else:
                seats[row - 1][column - 1] = class_name
                print(f"Reserving seat: row {row} column {column}")
                break
        except ValueError:
            print("Invalid input. Please enter valid row and column numbers.")

def main():
    while True:
        display_menu()
        choice = input("Please select an option: ").upper()

        if choice == 'F':
            reserve_seat("First Class")
        elif choice == 'B':
            reserve_seat("Business Class")
        elif choice == 'E':
            reserve_seat("Economy Class")
        elif choice == 'Q':
            break
        else:
            print("Invalid choice!")

    # Calculate total seats and reserved seats
    total_seats = FIRST_CLASS_CAPACITY + BUSINESS_CLASS_CAPACITY + ECONOMY_CLASS_CAPACITY
    reserved_seats = sum(1 for row in seats for seat in row if seat)

    print(f"\nReservation Type: {choice}")
    print(f"Total number of seats: {total_seats}")
    print(f"Total number of seats reserved: {reserved_seats}")

if __name__ == "__main__":
    main()
