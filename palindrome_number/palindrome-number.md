## Problem3(**Palindrome Number)**:

Given an integer `x`, return `true` *if* `x` *is a **palindrome**, and* `false` *otherwise*.

### **Solution:**

### 1.Sring Conversion:

```python
def isPalindrome(x):
    if x < 0:             # # Negative numbers are not palindrome
        return False
    y = str(x)
    return y == y[::-1]   # This is Python’s slice notation with three parts: y[start:stop:step]
                          # start: where to begin (left empty → start at the end)
                          # stop: where to end (left empty → go all the way)
                          # step: how to move (here: -1 means go backwards)
```

### 2.Math

```python
def isPalindrome(x):
    # Step 1: Negative numbers are never palindromes
    # (because of the '-' sign, which doesn't appear at the end when reversed)
    if x < 0:
        return False

    # Step 2: Store the original number to compare later
    original = x

    # Step 3: Initialize a variable to hold the reversed number
    reversed_num = 0

    # Step 4: Reverse the digits of the number
    while x > 0:
        digit = x % 10                # Get the last digit of x
        reversed_num = reversed_num * 10 + digit  # Shift left and add digit
        x = x // 10                   # Remove the last digit from x

    # Step 5: Check if the reversed number is the same as the original
    return original == reversed_num
