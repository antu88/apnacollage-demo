class MovieHall:
    def __init__(self, name, rows=5, cols=5):
        self.name = name
        self.rows = rows
        self.cols = cols
        self.seats = [["O" for _ in range(cols)] for _ in range(rows)]  # 'O' for Open seat

    def display_seats(self):
        print(f"\n🎬 Seating layout for {self.name} (O = Available, X = Booked):")
        print("   " + " ".join([f"{i+1:>2}" for i in range(self.cols)]))
        for idx, row in enumerate(self.seats):
            row_label = chr(65 + idx)  # A, B, C...
            print(f"{row_label}  " + "  ".join(row))
        print()

    def book_seat(self, seat_label):
        try:
            row_char, col_num = seat_label[0].upper(), int(seat_label[1:]) - 1
            row = ord(row_char) - 65
            if 0 <= row < self.rows and 0 <= col_num < self.cols:
                if self.seats[row][col_num] == "O":
                    self.seats[row][col_num] = "X"
                    print(f"✅ Seat {seat_label.upper()} booked successfully!")
                else:
                    print("❌ Seat already booked!")
            else:
                print("❌ Invalid seat number!")
        except (IndexError, ValueError):
            print("❌ Invalid input format! Use format like A1, B3, etc.")

    def available_seats_count(self):
        return sum(row.count("O") for row in self.seats)


def show_menu():
    print("\n🎟️ Movie Ticket Booking System 🎟️")
    print("1. View available seats")
    print("2. Book a seat")
    print("3. Show available seat count")
    print("4. Exit")


def main():
    hall = MovieHall("Grand Cinema", 5, 5)
    while True:
        show_menu()
        choice = input("Enter your choice (1-4): ").strip()

        if choice == '1':
            hall.display_seats()

        elif choice == '2':
            hall.display_seats()
            seat = input("Enter seat (e.g., A1, B2): ").strip()
            hall.book_seat(seat)

        elif choice == '3':
            count = hall.available_seats_count()
            print(f"🪑 Available seats: {count}")

        elif choice == '4':
            print("👋 Thank you for using the system. Enjoy your movie!")
            break

        else:
            print("❌ Invalid choice. Please enter a number between 1 and 4.")

# Run the system
if __name__ == "__main__":
    main()
