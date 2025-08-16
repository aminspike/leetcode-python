## Problem 6 (Valid Palindrome)

A phrase is a **palindrome** if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

```python
def isPalindrome(s):
    """
    Check if a given string is a valid palindrome.
    A valid palindrome ignores cases and non-alphanumeric characters.
    """

    # Step 1: Normalize the string
    # - Keep only alphanumeric characters (letters + numbers)
    # - Convert them to lowercase so that comparisons are case-insensitive
    cleaned = ''.join(ch.lower() for ch in s if ch.isalnum())
    # .isalnum(): It returns True if the string consists only of alphanumeric characters
    # (letters A–Z, a–z, and digits 0–9) and is not empty. Otherwise, it returns False.
    # str.join(iterable) is a string method that concatenates (glues together) the 
    # elements of an iterable (like a list, tuple, or generator) into a single string,
    # with the string you call it on used as the separator.

    # Step 2: Check if the cleaned string is the same forwards and backwards
    # - s[::-1] creates a reversed copy of the string
    return cleaned == cleaned[::-1]

```
