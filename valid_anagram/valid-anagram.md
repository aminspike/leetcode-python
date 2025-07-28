## Problem2(**Valid Anagram)**:

Given two strings `s` and `t`, return `true` if `t` is an anagram of `s`, and `false` otherwise.

### **Solution:**

```python
def isAnagram(s, t):
    # Step 1: If the lengths are different, they can't be anagrams
    if len(s) != len(t):
        return False

    # Step 2: Count how many times each character appears in string s
    count = {}
    for char in s:
        if char in count:
            count[char] += 1  # If the character is already in the dictionary, increase its count
        else:
            count[char] = 1   # If it's the first time we see this character, set count to 1

    # Step 3: Go through string t and subtract from the counts
    for char in t:
        if char not in count:
            # If t contains a character that s does not have, it's not an anagram
            return False
        if count[char] == 0:
            # If we already used up all of this character, t has too many → not an anagram
            return False
        count[char] -= 1  # Subtract 1 because we've "used" one instance of this character

    # Step 4: If we never returned False, it means all counts matched up correctly
    return True

``` 
