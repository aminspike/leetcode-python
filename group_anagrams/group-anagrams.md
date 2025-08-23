## Problem 10 (Group Anagrams)

Given an array of strings `strs`, group the anagrams together. You can return the answer in **any order**.

### Solution 1 (Sorted String Approach)

```python
from collections import defaultdict

def groupAnagrams(strs):
    anagrams = defaultdict(list)  # key -> list of words

    for word in strs:
        # 1. Sort characters of the word -> unique signature
        key = ''.join(sorted(word))  
        # sorted() alone gives us a list (not usable as a dict key).
        # .join() converts that list into a string (usable as a dict key).
        
        # if we didn't use defaultdict(list) this line would be added:
        # if key not in anagrams:
            # anagrams[key] = []
        
        # 2. Add word into the correct bucket
        anagrams[key].append(word)

    # 3. Return grouped anagrams
    return list(anagrams.values())
```

### `defaultdict()`

`defaultdict` is a special type of dictionary from the `collections` module. When you create `defaultdict(list)` You’re saying: 
“If the key doesn’t exist yet, automatically create it with a default value of an empty list (`[]`).”
If you used a normal dictionary: `anagrams = {}` and then try:

```python
anagrams["aet"].append("eat")
```

Python would give you an **error** because `"aet"` is not yet a key in the dictionary. but with `defaultdict` it works perfectly the first time because `"aet"` automatically starts as an empty list `[]`.

```python
**from collections import defaultdict

anagrams = defaultdict(list)

anagrams["aet"].append("eat")   # no error, creates {"aet": ["eat"]}
anagrams["aet"].append("tea")   # {"aet": ["eat","tea"]}
anagrams["abt"].append("bat")   # {"aet": ["eat","tea"], "abt": ["bat"]}**
```

### Solution 2 (**Frequency Count Approach (faster))**

```python
from collections import defaultdict

def groupAnagrams(strs):
    anagrams = defaultdict(list)  # key -> list of words

    for word in strs:
        # Count frequency of each letter
        count = [0] * 26    # count is a list of 26 zeros (for 26 letters a–z).
        for ch in word:
            count[ord(ch) - ord('a')] += 1   
            # ord(ch) - ord('a') converts a character into an index 0–25.
            # ord() returns the ASCII (or Unicode) number of a character.
            # ord('a')  # 97
            # ord('b')  # 98
            # ord('A')  # 65

        # Use tuple as dict key
        key = tuple(count)
        # Lists cannot be dictionary keys because they are mutable.
        # Tuples can be dictionary keys (hashable).
        # Now key is something like (1,0,0,0,1,0,...,1,...).

        # Append word to its group
        anagrams[key].append(word)

    # Return grouped anagrams
    return list(anagrams.values())
```
