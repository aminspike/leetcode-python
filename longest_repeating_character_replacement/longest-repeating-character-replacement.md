## **Problem 9 (Longest Repeating Character Replacement)**

You are given a string `s` and an integer `k`. You can choose any character of the string and change it to any other uppercase English character. You can perform this operation at most `k` times.

Return *the length of the longest substring containing the same letter you can get after performing the above operations*.

```python
def characterReplacement(self, s, k):
    """
    :type s: str
    :type k: int
    :rtype: int
    """
    # Dictionary to store counts of characters in the current window
    count = {}
    
    # Max frequency of any single character in the current window
    max_freq = 0
    
    # Left pointer of the sliding window
    left = 0
    
    # Best (maximum) length of valid window found so far
    best_len = 0

    # Expand the window by moving 'right' pointer
    for right in range(len(s)):
        char = s[right]
        
        # Add current character to the window count
        count[char] = count.get(char, 0) + 1
        
        # Update the max frequency character in the window
        # (used to decide if the window is valid)
        max_freq = max(max_freq, count[char])
        
        # If the window is invalid (needs more than k replacements)
        # shrink from the left until it's valid again
        while (right - left + 1) - max_freq > k:
            char_left = s[left]
            count[char_left] -= 1
            if count[char_left] == 0:
                # Clean up dictionary to save space
                del count[char_left]
            left += 1  # move left pointer forward
        
        # Update the best length found so far
        best_len = max(best_len, right - left + 1)

    # Return the maximum length of valid substring found
    return best_len

```
