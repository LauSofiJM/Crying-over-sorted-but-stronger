# Crying over sorted but stronger

***
### Better Comments
_This is the how I decided to use the extension._
- #Info related to the program (grey)
- #* Titles (green light)
- #? Advices or clarifications (blue)
- #todo Need to reforce (orange)
- #! Confused bout' something (red)
- #// Discarted (--)
- #- Success (yellow)
***
## 1. Basic operations
In this opportunity, I had to make some adjustments to the code, but I kept the same logic and structure.

```python

#* Basic operations
# I need to create a function that allows people to do basic operations (+, -, *, /) using two numbers.

def basic_operations(num1, num2, operation):
    try:
        if operation == "+":
            print(f"\nThe result is: {num1 + num2}")
        elif operation == "-":
            print(f"\nThe result is: {num1 - num2}")
        elif operation == "*":
            print(f"\nThe result is: {num1 * num2}")
        elif operation == "/":
            if num2 != 0:
                try:
                    print(f"\nThe result is:  {num1 // num2}")
                except ZeroDivisionError:
                    num2 = float(input("\nYou can not divide by zero. Enter the second number: "))
            else:
                raise ValueError("The second number cannot be zero.")
        else:
            raise ValueError("Enter a valid operation symbol (+, -, *, /).")
    except ValueError as e:
        print(e)

num1 = float(input("Enter the first number: "))
num2 = float(input("\nEnter the second number: "))
operation = input("\nEnter the operation symbol (+, -, *, /): ")
result = basic_operations(num1, num2, operation) #todo I need to study more about functions and return values.
```
___
## 2. Palindrome or not?
I decided to experiment with using a try-except block with lowercase letters, but ultimately found it unnecessary.

```python

#* Palindrome or not?
#A palindrome is a sequence of characters which reads the same forward and backward.


#* Palindrome or not?
#A palindrome is a sequence of characters which reads the same forward and backward.

def palindrome(word):
    try:
        word = word.lower() # Convert the word to lowercase to avoid errors when comparing the letters.
        lst = []
        for letter in word:
            lst.append(letter) # Convert the word to a list to compare the letters.
        for i in range(len(lst)//2): # If it is a palindrome, its first half will be the same as the second half.
            if lst[i] != lst[-i-1]:
                return False
        return True
    except:
        return False

word = input("Enter a word: ")
if palindrome(word):
    print(f"\n{word} is a palindrome.")
else:
    print(f"\n{word} is not a palindrome.")
```
___
## 3. Prime numbers
The code alredy had the most important exception.

```python

#* Prime number
#A prime number is a natural number greater than 1 that is not a product of two smaller natural numbers

def is_prime(num): #! I found this way to check if a number is prime in a website. It is more efficient than the one I was using.
    if num <= 1:
        return False
    for i in range(2, int(num**0.5) + 1): #? I need to check if the number is divisible by any number from 2 to the square root of the number.
        if num % i == 0:
            return False
    return True

def get_numbers():
    numbers = []
    while True:
        number = input("Enter an integer (or press 'q' to quit): ") #? I didn't want the user to write a specific number for the list to accept.
        if number.lower() == 'q':
            break
        try:
            number = int(number)
            numbers.append(number)
        except ValueError:
            print("Invalid input. Please enter an integer or 'q' to quit.")
    return numbers

def get_prime():
    numbers = get_numbers()

    prime_numbers = []
    for number in numbers:
        if is_prime(number):
            prime_numbers.append(number)

    prime_numbers.sort() #? I used the sort function to organize the numbers in ascending order.
    prime_numbers = set(prime_numbers) #? I used the set function to avoid repeated numbers.

    return prime_numbers

prime_numbers = get_prime()
print("Prime numbers:", prime_numbers)
```
___
## 4. Greater sum

I used Try - except back then when I wrote the code so it was kinda usefull. I just had to add the other ValueError.

```python

#* Greater sum of two numbers
#I need to create a function that receives a list of numbers and returns greater sum of two consecutive numbers.

def get_numbers(): #? I reused the get_numbers function from Prime_Numbers.py.
    numbers = []
    while True:
        number = input("Enter an integer (or press 'q' to quit): ")
        if number.lower() == 'q':
            break
        try:
            number = int(number)
            numbers.append(number)
        except ValueError:
            print("Invalid input. Please enter an integer or 'q' to quit.")
    numbers = list(set(numbers)) #? I used the set function to avoid repeated numbers.
    return numbers

try:
    def greater_sum(numbers):
        if len(numbers) < 2:
            return None  # Not enough numbers to calculate sum
        max_sum = numbers[0] + numbers[1]
        for i in range(1, len(numbers)-1):
            current_sum = numbers[i] + numbers[i+1]
            max_sum = max(max_sum, current_sum)
        return max_sum
except ValueError:
    print("You need to write at least two numbers.")

numbers = get_numbers()
result = greater_sum(sorted(numbers))
print("The numbers are:", numbers)
print("The greater sum of two consecutive numbers is:", result)
```
___
## 5. Anagrams
Adding the exception was not as hard as it could be thanks to the code that I had wrote.

```python

#* Anagrams
# I need to create a function that returns the anagrams found in a list of words and also I need to use exceptions to handle possible errors.

def get_words():
    while True:
        try:
            words = input("Write words separated by commas: ").split(',') #? Split the input by commas
            words = [word.strip() for word in words]
            if any(word.isdigit() for word in words): #? Check if there are numbers in the list
                raise ValueError("Please enter words only. Numbers are not allowed.") #? I used the ValueError exception to handle the error.
            else:
                break
        except ValueError as e:
            print(e)
    return words

def is_anagram(words):
    anagrams = set()
    for i in range(len(words)):
        for j in range(i+1, len(words)):
            if sorted(words[i]) == sorted(words[j]):
                anagrams.add(words[i])
                anagrams.add(words[j])
    return list(anagrams)

words = get_words()
print(f"\nThe original list is: {words}")
anagrams = is_anagram(words)
print(f"\nThe anagrams are: {anagrams}")
```
***

# Stronger Shape

***

### That was it. Thanks for reading.
