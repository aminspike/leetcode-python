**Problem**: Given an array of integers `nums` and an integer `target`, return *indices of the two numbers such that they add up to `target`*.

You may assume that each input would have ***exactly* one solution**, and you may not use the *same* element twice.

You can return the answer in any order.

### **Solution:**

### **1.Brute Force**

using two nested loops to try every pair — **is called the *brute force* approach**. Loop through each element *x* and find if another value equals to *target*−*x*.
Try **all possible combinations** without any shortcuts or optimizations.

It’s simple, often the easiest to write, but not the most efficient.

```python
def twoSum(nums, target):
    for i in range(len(nums)):  # goes through each index i in the list.
        for j in range(i + 1, len(nums)):  # this is a nested loop that starts from the element after i.
                                           # It prevents repeating the same pair and avoids i == j.
                                           # For each i, loop through every later index j.
            if nums[i] + nums[j] == target:
                return [i, j]
    return []  # This is a backup return, in case no two numbers add up to the target.
               # In LeetCode, this won’t be triggered because they promise exactly one solution.
```

### **2.Two-pass Hash Table**

A **hash table** (or dictionary in Python) is a way to store information so you can find it quickly.
Here, we store a number as the key and its index as the value.
**Step 1: First Pass — Build the hash table**
Go through the list of numbers one by one. Put each number and its index into the hash table.
**Step 2: Second Pass — Find the pair**
Go through the list again. For each number, calculate what other number you need to reach the target: `needed = target - current_number`. Check if `needed` is in the hash table. Also, make sure `needed` is not the same element (different index). If yes, return the two indexes.

```python

def twoSum(nums, target):
    # Step 1: build hash table
    num_to_index = {}
    for i, num in enumerate(nums): # Go through each number in the list, and give me both the number and its index.
        num_to_index[num] = i      # Save the number as a key, and its index as the value.

    # Step 2: find the pair
    for i, num in enumerate(nums):
        needed = target - num
        if needed in num_to_index and num_to_index[needed] != i: # we use != i because we don’t want to use the same number twice
            return [i, num_to_index[needed]]

    return []
```

### **3.Two-pass Hash Table**

**Instead of doing two loops**, we Loop through the list **once.** While looping, we **check** if the needed number is already in the hash table. If not, we **add the current number** to the hash table. So we build and use the hash table at the same time — **in one pass**.

```python
def twoSum(nums, target):
    num_to_index = {}  # this is our hash table

    for i, num in enumerate(nums):
        needed = target - num  # what number do we need?

        if needed in num_to_index:
            return [num_to_index[needed], i]

        num_to_index[num] = i  #  store this number with its index

```

Only one loop → O(n) time. Less code, more efficient. Finds the answer without finishing the loop. 
