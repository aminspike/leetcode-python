def strStr(haystack, needle):
    """
    Finds the index of the first occurrence of 'needle' in 'haystack'.
    Returns -1 if 'needle' is not found.

    Example:
        haystack = "sadbutsad", needle = "sad" → returns 0
        haystack = "leetcode", needle = "leeto" → returns -1
    """

    # We only need to check starting positions where 'needle' can fit completely.
    # If haystack length = H and needle length = N,
    # the last valid start index is H - N.
    for i in range(len(haystack) - len(needle) + 1):

        # range(i) --> 0, 1, ..., i-1
        # Take a slice from haystack starting at i, length = len(needle)
        # Example: haystack = "abcde", needle = "cd", i = 2
        #          haystack[2:4] → "cd"
        if haystack[i : i + len(needle)] == needle:
            return i  # Found a match at index i

    # If we finish the loop with no match, needle is not in haystack
    return -1



