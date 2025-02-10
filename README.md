import time
from functools import lru_cache

def fibonacci_generator():
    a, b = 0, 1
    while True:
        yield a
        a, b = b, a + b

def fibonacci_iterative(n):
    if n <= 0:
        return []
    elif n == 1:
        return [0]
    fib_seq = [0, 1]
    for _ in range(2, n):
        fib_seq.append(fib_seq[-1] + fib_seq[-2])
    return fib_seq

def fibonacci_recursive(n):
    if n <= 1:
        return n
    return fibonacci_recursive(n - 1) + fibonacci_recursive(n - 2)

@lru_cache(maxsize=None)
def fibonacci_memoized(n):
    if n <= 1:
        return n
    return fibonacci_memoized(n - 1) + fibonacci_memoized(n - 2)

def is_fibonacci(num):
    a, b = 0, 1
    while b < num:
        a, b = b, a + b
    return b == num

def main():
    print("Welcome to the Fibonacci Generator!")
    while True:
        print("\nChoose a method to calculate Fibonacci numbers:")
        print("1. Generator (Infinite series)")
        print("2. Iterative (First N terms)")
        print("3. Recursive (Nth term)")
        print("4. Memoized Recursive (Nth term)")
        print("5. Check if a number is Fibonacci")
        print("6. Exit")

        choice = input("Enter your choice (1/2/3/4/5/6): ")

        if choice == '1':
            print("Using Generator. Generating Fibonacci numbers...")
            gen = fibonacci_generator()
            try:
                count = int(input("How many Fibonacci numbers do you want to generate? "))
                if count <= 0:
                    print("Please enter a positive integer.")
                    continue
                for _ in range(count):
                    print(next(gen), end=" ")
                print()
            except ValueError:
                print("Invalid input! Please enter a valid integer.")

        elif choice == '2':
            try:
                n = int(input("Enter the number of terms: "))
                if n <= 0:
                    print("Please enter a positive integer.")
                    continue
                start_time = time.time()
                fib_seq = fibonacci_iterative(n)
                end_time = time.time()
                print(f"Fibonacci Series (First {n} terms): {fib_seq}")
                print(f"Time taken: {end_time - start_time:.6f} seconds")
            except ValueError:
                print("Invalid input! Please enter a valid integer.")

        elif choice == '3':
            try:
                n = int(input("Enter the term number (Nth term): "))
                if n < 0:
                    print("Please enter a non-negative integer.")
                    continue
                start_time = time.time()
                result = fibonacci_recursive(n)
                end_time = time.time()
                print(f"The {n}th Fibonacci number is: {result}")
                print(f"Time taken: {end_time - start_time:.6f} seconds")
            except ValueError:
                print("Invalid input! Please enter a valid integer.")

        elif choice == '4':
            try:
                n = int(input("Enter the term number (Nth term): "))
                if n < 0:
                    print("Please enter a non-negative integer.")
                    continue
                start_time = time.time()
                result = fibonacci_memoized(n)
                end_time = time.time()
                print(f"The {n}th Fibonacci number is: {result}")
                print(f"Time taken: {end_time - start_time:.6f} seconds")
            except ValueError:
                print("Invalid input! Please enter a valid integer.")

        elif choice == '5':
            try:
                num = int(input("Enter a number to check if it's a Fibonacci number: "))
                if is_fibonacci(num):
                    print(f"{num} is a Fibonacci number.")
                else:
                    print(f"{num} is not a Fibonacci number.")
            except ValueError:
                print("Invalid input! Please enter a valid integer.")

        elif choice == '6':
            print("Exiting the program. Goodbye!")
            break

        else:
            print("Invalid choice! Please try again.")

if __name__ == "__main__":
    main()
