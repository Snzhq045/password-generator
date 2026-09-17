import random
import string

def generate_password(length=12, use_digits=True, use_special=True):
    """Генерация надежного случайного пароля."""
    letters = string.ascii_letters
    digits = string.digits if use_digits else ""
    special = "!@#$%^&*()_+-=" if use_special else ""
    
    all_chars = letters + digits + special
    if not all_chars:
        return ""
    
    # Гарантируем наличие хотя бы одного символа каждого выбранного типа
    password = []
    password.append(random.choice(string.ascii_lowercase))
    password.append(random.choice(string.ascii_uppercase))
    if use_digits:
        password.append(random.choice(digits))
    if use_special:
        password.append(random.choice(special))
        
    # Заполняем оставшуюся длину
    while len(password) < length:
        password.append(random.choice(all_chars))
        
    random.shuffle(password)
    return "".join(password)

def main():
    print("=== Secure Password Generator CLI ===")
    try:
        length = int(input("Введите длину пароля (по умолчанию 12): ") or 12)
        use_digits = input("Включать цифры? (y/n, по умолчанию y): ").lower() != 'n'
        use_special = input("Включать спецсимволы? (y/n, по умолчанию y): ").lower() != 'n'

        if length < 4:
            print("Ошибка: Длина пароля должна быть не менее 4 символов.")
            return

        password = generate_password(length, use_digits, use_special)
        print("\n--------------------------------")
        print(f"Сгенерированный пароль: {password}")
        print("--------------------------------")

    except ValueError:
        print("Ошибка ввода. Пожалуйста, вводите числовые значения для длины.")

if __name__ == "__main__":
    main()
