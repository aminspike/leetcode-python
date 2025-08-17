## Problem 7 (**Longest Substring Without Repeating Characters**)

Given a string `s`, find the length of the **longest** **substring** without duplicate characters.

### Solution 1 (Brute Force)

Works fine for small strings (say < 500 chars) but slow.

```python
def length_of_longest_substring(s):
    best_len = 0
    n = len(s)

    for i in range(n):
        for j in range(i+1, n+1):   # 🔥 must start at i+1, go up to n (inclusive end)
            substring = s[i:j]
            # uniqueness check: convert to set (removes duplicates)
            if len(set(substring)) == len(substring):
                best_len = max(best_len, j - i)
    return best_len
```

### Solution 2 (Sliding Window With a Set)

- **`L` and `R` are like scissors cutting a piece of the string.**
- You expand `R` one step at a time.
- If there’s a duplicate, you slide `L` forward until it’s unique again.
- The biggest piece you ever get is the answer.

```python
def length_of_longest_substring(s):
    seen = set()        # keeps track of chars in the current window
    L = 0               # left boundary of the window
    best_len = 0        # the maximum length found

    for R in range(len(s)):              # R is the right boundary of the window
        while s[R] in seen:              # ensures the window never has duplicates.
            seen.remove(s[L])            # remove the leftmost char
            L += 1                       # shrink window from the left
        seen.add(s[R])                   # add the new char (unique now)
        best_len = max(best_len, R - L + 1)  # update max length

    return best_len
```

### Solution 3 (Sliding Window With Last-seen Map)

```python
def lengthOfLongestSubstring(s):
    # Dictionary to store the last index where each character was seen
    last_seen = {}

    # Left pointer of our sliding window
    L = 0

    # Best length found so far
    best_len = 0

    # Iterate with the right pointer (R) through each character
    for R, char in enumerate(s):

        # If we’ve seen this character before
        # AND its last index is within the current window [L..R]
        # → we must move L forward to skip the duplicate
        if char in last_seen and last_seen[char] >= L:
            L = last_seen[char] + 1   # jump L right past the duplicate

        # Update the last seen index of the current character
        last_seen[char] = R

        # Window size = R - L + 1
        best_len = max(best_len, R - L + 1)

    return best_len

```
