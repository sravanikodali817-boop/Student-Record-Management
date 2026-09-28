import re

FILE_NAME = "students.txt"


# Validate email using Regex
def validate_email(email):
    pattern = r"^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$"
    return re.match(pattern, email)


# Add Student
def add_student():
    try:
        student_id = int(input("Enter Student ID: "))
        name = input("Enter Student Name: ")
        email = input("Enter Email: ")

        # Validate email
        if not validate_email(email):
            raise ValueError("Invalid email format!")

        # Save student data to file
        with open(FILE_NAME, "a") as file:
            file.write(f"{student_id},{name},{email}\n")

        print("Student added successfully!")

    except ValueError as e:
        print("Error:", e)

    except IOError as e:
        print("File error:", e)


# Read Student Data
def read_students():
    try:
        with open(FILE_NAME, "r") as file:
            print("\n--- Student Records ---")

            records = file.readlines()

            if not records:
                print("No student records found.")
                return

            for record in records:
                student_id, name, email = record.strip().split(",")

                print(f"ID: {student_id}, Name: {name}, Email: {email}")

    except FileNotFoundError:
        print("No student records found.")

    except IOError as e:
        print("File error:", e)


# Main Program
def main():
    while True:
        print("\n===== Student Record Manager =====")
        print("1. Add Student")
        print("2. Read Student Data")
        print("3. Exit")

        try:
            choice = int(input("Enter your choice: "))

            if choice == 1:
                add_student()

            elif choice == 2:
                read_students()

            elif choice == 3:
                print("Program exited.")
                break

            else:
                raise ValueError("Please enter a choice between 1 and 3.")

        except ValueError as e:
            print("Error:", e)


# Start the program
if __name__ == "__main__":
    main()