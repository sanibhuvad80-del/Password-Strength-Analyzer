import re
import random
import string

# List of common weak passwords
common_passwords = [
    "password",
    "123456",
    "qwerty",
    "admin",
    "welcome"
]

# Function to check password strength
def check_password(password):

    score = 0

    # Check length
    if len(password) >= 8:
        score += 1

    # Check lowercase letters
    if re.search("[a-z]", password):
        score += 1

    # Check uppercase letters
    if re.search("[A-Z]", password):
        score += 1

    # Check numbers
    if re.search("[0-9]", password):
        score += 1

    # Check special characters
    if re.search("[!@#$%^&*]", password):
        score += 1

    # Check common passwords
    if password.lower() in common_passwords:
        return "Weak"

    # Decide strength level
    if score <= 2:
        return "Weak"
    elif score <= 4:
        return "Moderate"
    else:
        return "Strong"

# Function to generate strong password
def generate_password(length=12):

    characters = (
        string.ascii_letters +
        string.digits +
        "!@#$%^&*"
    )

    password = ""

    for i in range(length):
        password += random.choice(characters)

    return password

# Main Program
user_password = input("Enter your password: ")

strength = check_password(user_password)

print("\nPassword Strength:", strength)

if strength != "Strong":
    print("Suggested Strong Password:")
    print(generate_password())
