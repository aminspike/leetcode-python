## Problem 11 (**Top K Frequent Elements)**

Given an integer array `nums` and an integer `k`, return *the* `k` *most frequent elements*. You may return the answer in **any order**.

### Solution 1 (Not good enough-slow)

```python
def topKFrequent(nums, k):
    freqs = {}
    for num in nums:
        if num in freqs:
            freqs[num] += 1
        else:
            freqs[num] = 1

    # Sort the items once by frequency (descending)
    sorted_items = sorted(freqs.items(), key=lambda x: x[1], reverse=True)
    # .items() turns freqs dictionary into a list of (key, value) pairs
    # In Python, many functions (sorted(), min(), max(), etc.) accept a key argument.
    # The key tells Python what value to use when comparing items.
    # lambda creates a small anonymous function in one line. General form:
       # lambda arguments: expression
    # So lambda x: x[1] means:
       # Input: a tuple x (like (3, 5))
       # Output: x[1] (the second element, e.g., 5)
    # By default, Python sorts in ascending order. reverse=True makes it descending.   

    # Extract the first k keys using list comprehension
    output_list = [num for num, _ in sorted_items[:k]]
    return output_list
```

### Solution 1 (Optimized)

```python
from collections import defaultdict

class Solution(object):
    def topKFrequent(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: List[int]
        """
        popCount = defaultdict(int)
        # defaultdict(int) → automatically starts counts at 0, so no if/else is needed.
        # Normal dict → you must check if key exists.
        # defaultdict(int) → missing keys default to 0, so you can increment directly.
        for n in nums:
            popCount[n] += 1

        sPopCount = sorted(popCount, key=popCount.get, reverse=True)
        return [sPopCount[i] for i in range(k)]
```

### **Solution 2 (Bucket sort approach** (best for this problem))

```python
from collections import Counter

def topKFrequent(nums, k):
    freqs = Counter(nums)  # creates a dictionary of number → frequency.
    
    # We make a list of empty lists, one for each possible frequency.
    bucket = [[] for _ in range(len(nums)+1)
    # Why len(nums)+1? beacause if we use len(nums) the index wil be (0, len(num)-1).
    # But with len(nums)+1 we will have (0, len(nums)) index.
    # Index 0 will never be used (since no element has frequency 0), but it’s a simple
    # way to guarantee space for all possible frequencies.
    # Example for len(nums) = 6:
        # bucket = [ [], [], [], [], [], [], [] ]
    
    # Place numbers into their frequency bucket    
    for num, count in freqs.items():
        bucket[count].append(num)
        # Example:
        # Number 1 has frequency 3 → bucket[3] = [1]
        # Number 2 has frequency 2 → bucket[2] = [2]
        # Number 3 has frequency 1 → bucket[1] = [3]
        # bucket = [ [], [3], [2], [1], [], [], [] ]

        
      

    res = []
    for i in range(len(bucket)-1, 0, -1):
    # In Python, range(a, b, c) means:
        # Start at a → Start at the last index (len(bucket)-1)
        # Stop before b(b is excluded) → Go down to 1 (because stop=0, but 0 is excluded)
        # Increase/decrease by c each step → Step = -1 (go backwards)
        
        for num in bucket[i]:
            res.append(num)
            if len(res) == k:
                return res

```

### **Solution 3 (heap-based)**

```python
import heapq
from collections import Counter

def topKFrequent(nums, k):
    freqs = Counter(nums)
    return [num for num, _ in heapq.nlargest(k, freqs.items(), key=lambda x: x[1])]
    # heapq.nlargest finds the k largest elements from an iterable.
```

### Comparison

| Solution | Counting | Top-k selection | Complexity | Notes |
| --- | --- | --- | --- | --- |
| Solution 1 `while max()` | O(n) | O(n·k) | O(n·k) | Slow for large k |
| Solution 1 (optimized) | O(n) | O(n log n) | O(n log n) | Fast and simple |
| Bucket sort | O(n) | O(n) | O(n) | Optimal for large n, k small |
| heap | O(n) | O(n log k) | O(n log k) | Fastest in Python, very clean |
