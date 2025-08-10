## Problem 5 (**Longest Common Prefix)**

Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string `""`.

### Solution 1 (Horizontal Scanning or Shrink Prefix)

Compare prefixes between the first string and each subsequent string one by one.
Gradually shorten the prefix until all strings match it.

```python
def longestCommonPrefix(strs):
    """
    Finds the longest common prefix (beginning part) of all strings in the list.
    Example: ["flower", "flow", "flight"] → "fl"
    """

    # If the list is empty, there is no common prefix
    if not strs:   # is a quick way in Python to check “is the list empty?”
        return ""
    # Why we need it here? If strs is empty and we try prefix = strs[0], 
    # Python will crash 
     
    # Start by assuming the first word is the prefix
    prefix = strs[0]

    # Go through each of the remaining words one by one
    for word in strs[1:]:
        # While the current word does NOT start with our prefix,
        # remove the last character from prefix
        while not word.startswith(prefix):
            prefix = prefix[:-1]  # Remove the last character
                                  # Python’s string slicing(The special case: [:-1])
                                  # means slice from the start (index 0) up to (but not
                                  # including) the last character
            # If prefix becomes empty, no common prefix exists
            if prefix == "":
                return ""

    # After we have checked all words, return what is left in prefix
    return prefix

```

### Solution 2 (Vertical Scanning)

Instead of checking whole prefixes, check character-by-character **across all strings at once.**

- Check first character of all strings — if all match, keep going
- Check second character of all strings — if all match, continue
- Stop when a mismatch or end of any string occurs

```python
def longestCommonPrefix(strs):
    # If the list is empty, there is no common prefix
    if not strs:
        return ""

    # Loop through each character index of the first word
    for i in range(len(strs[0])):
        # Take the character at position i from the first word
        char = strs[0][i]

        # Compare this character with the same position in all other words
        for string in strs[1:]:
            # If we reach the end of a word OR a mismatch occurs
            if i == len(string) or string[i] != char:
                # Return the prefix found so far (up to index i)
                return strs[0][:i]

    # If we finish the loop with no mismatches,
    # the entire first word is the common prefix
    return strs[0]

```
