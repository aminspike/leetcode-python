## Problem 8 (**Permutation in String)**

Given two strings `s1` and `s2`, return `true` if `s2` contains a permutation of `s1`, or `false` otherwise.

In other words, return `true` if one of `s1`'s permutations is the substring of `s2`.

```python
def checkInclusion(s1, s2):
    n, m = len(s1), len(s2)
    if n > m:
        return False

    # Step 1: Build frequency dict for s1
    s1_count = {}
    for ch in s1:
        s1_count[ch] = s1_count.get(ch, 0) + 1
        # get(key, default) is a dictionary method.It returns the value for key if it 
        # exists. If key doesn’t exist, it returns default instead.
 
    # Step 2: Build frequency dict for the first window of s2
    # We build the first window of length n in s2.
    window_count = {} # window_count keeps track of how many times each character appears.
    for i in range(n):
        ch = s2[i]
        window_count[ch] = window_count.get(ch, 0) + 1

    # Step 3: Slide the window across s2
    for i in range(m - n + 1):     # i = starting index of the current window.
                                   # We loop through all possible windows of size n in s2
        # Compare current window with s1
        if window_count == s1_count:
            return True

        # Move the window: remove leftmost, add rightmost
        if i + n < m:   # ensure we don't go out of range
                        # i + n = index of the new character that will enter the window.
            left_char = s2[i]
            right_char = s2[i + n]

            # Remove left char
            window_count[left_char] -= 1
            if window_count[left_char] == 0:
                del window_count[left_char]

            # Add right char
            window_count[right_char] = window_count.get(right_char, 0) + 1

    return False

```

Use `collections.Counter` instead of manual dict:

```python
from collections import Counter

def checkInclusion(self, s1, s2):
    n, m = len(s1), len(s2)
    if n > m:
        return False

    s1_count = Counter(s1) 
    window_count = Counter(s2[:n])
    # Counter is a special dictionary from Python’s collections module.
    # It counts how many times each element appears in an iterable.

    for i in range(m - n + 1):
        if window_count == s1_count:
            return True

        if i + n < m:
            left_char = s2[i]
            right_char = s2[i + n]

            window_count[left_char] -= 1
            if window_count[left_char] == 0:
                del window_count[left_char]

            window_count[right_char] += 1

    return False
```
