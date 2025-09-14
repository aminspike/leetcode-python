## Problem 12 (Ransom Note)

Given two strings `ransomNote` and `magazine`, return `true` *if* `ransomNote` *can be constructed by using the letters from* `magazine` *and* `false` *otherwise*.

Each letter in `magazine` can only be used once in `ransomNote`.

### Solution 1 (using arrays)

- Uses **direct indexing** (`ord(c) - ord('a')`) → O(1) operations.
- Very **cache-friendly** (all values stored in a compact block).
- Constant space = 26 integers, no matter the input size.
- **Fastest option** when you know inputs are only lowercase English letters.

```python
def canConstruct(ransomNote: str, magazine: str) -> bool:
    # frequency array for 'a' to 'z'
    freq = [0] * 26  
    
    # count letters in magazine
    for c in magazine:
        freq[ord(c) - ord('a')] += 1
    
    # check letters in ransomNote
    for c in ransomNote:
        idx = ord(c) - ord('a')
        freq[idx] -= 1
        if freq[idx] < 0:  # not enough of this char
            return False
    
    return True

```

### Solution 2 (using dictionaries)

If characters aren’t guaranteed to be lowercase letters:

- Uses **hashing** for lookups and updates.
- Average O(1), but slightly slower than arrays due to hashing overhead.
- Space usage grows with the number of distinct characters.
- More flexible (works with any characters, not just `a`–`z`).

```python
def canConstruct(ransomNote: str, magazine: str) -> bool:
    freq = {}
    
    for c in magazine:
        freq[c] = freq.get(c, 0) + 1
    
    for c in ransomNote:
        if freq.get(c, 0) == 0:
            return False
        freq[c] -= 1
    
    return True
```
