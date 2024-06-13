---
title: Strings and HashMap
description: Top K Elements in List.
date: '2024-6-9'
categories:
  - LeetCode
  - Java
  - Python
published: true
---

## Problems List

- [Top K Elements in List](#top-k-elements-in-list)
- [Best Time to Buy and Sell Stock](#best-time-to-buy-and-sell-stock)

## Top K Elements in List

[Link to the Problem](https://neetcode.io/problems/top-k-elements-in-list)

In this problem we want to find the `k` most frequently occurring numbers in a list called `nums`.


**Solution in Python**
```python
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        #declaring a empty directory which stores the key and the value
        count = {}    
        #Creating a freq bucket
        freq = [[] for i in range(len(nums) + 1)]

        #counting the number of times each value occurs in nums 
        for n in nums:
            #dictionary.get(key, value)
            count[n] = 1 + count.get(n, 0)

        for n, c in count.items():
            freq[c].append(n)

        res = []

        for i in range(len(freq)-1, 0, -1):
            for n in freq[i]:
                res.append(n)
                if len(res) == k:
                    return res
```
*Time Complexity = O(n)* <br/>
*Space Complexity = O(n)*


## Step-by-Step Explanation

In this blog, we'll break down the `topKFrequent` function line by line to understand how it works. We'll visualize each step to make it easier to grasp.

### Example:
- **nums = [1, 1, 2, 2, 2, 3, 3, 4]**
- **k = 2**

### 1. Class and Function Definition

```python
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
```

- `class Solution:` This defines a new type of object called `Solution`.
- `def topKFrequent:` This starts a function inside our `Solution` class.
- `self:` This refers to the instance of the class itself.
- `nums:` This is a list of numbers that we are given.
- `k:` This is a number that tells us how many of the most frequent numbers we want to find.
- `List[int]:` This indicates that `nums` is a list of integers, and the function will return a list of integers.

### 2. Create a Count Dictionary

```python
count = {}
```

- `count = {}`: This creates an empty dictionary called `count`.

### 3. Create Frequency Buckets

```python
freq = [[] for i in range(len(nums) + 1)]
```

- `freq = [[] for i in range(len(nums) + 1)]:` Since `len(nums) = 8`, we create a list with 9 empty lists inside it.
  ```python
  freq = [[], [], [], [], [], [], [], [], []]
  ```

### 4. Count Occurrences of Each Number

```python
for n in nums:
    count[n] = 1 + count.get(n, 0)
```

- `for n in nums:` This loop goes through each number (`n`) in the list `nums`.
- `count[n] = 1 + count.get(n, 0):`
  - `count.get(n, 0):` This looks in the `count` dictionary for the number `n`. If `n` is already in `count`, it returns its value. If `n` is not in `count`, it returns 0.
  - `1 + count.get(n, 0):` Adds 1 to the current count of `n` (or to 0 if `n` wasn't there before).
  - `count[n] = ...:` This updates the dictionary to reflect the new count for `n`.

### Visualization of Count Dictionary:

After iterating through `nums = [1, 1, 2, 2, 2, 3, 3, 4]`:
```
count = {1: 2, 2: 3, 3: 2, 4: 1}
```
This means:
- Number `1` appears 2 times.
- Number `2` appears 3 times.
- Number `3` appears 2 times.
- Number `4` appears 1 time.

### 5. Fill Frequency Buckets

```python
for n, c in count.items():
    freq[c].append(n)
```

- `for n, c in count.items():` This loop goes through each key-value pair in the `count` dictionary. Here, `n` is the number, and `c` is how many times it appears.
- `freq[c].append(n):` This takes the number `n` and puts it into the bucket `c` in `freq`.

### Visualization of Frequency Buckets:

After filling based on `count`:
```
freq = [[], [4], [1, 3], [2], [], [], [], [], []]
```
This means:
- `Bucket 0:` Empty (No numbers appear 0 times)
- `Bucket 1:` [4] (Number 4 appears 1 time)
- `Bucket 2:` [1, 3] (Numbers 1 and 3 appear 2 times)
- `Bucket 3:` [2] (Number 2 appears 3 times)
- `Bucket 4 and beyond:` Empty (No numbers appear more than 3 times in this example)

### 6. Prepare Result List

```python
res = []
```

- `res = []:` This creates an empty list called `res`. This will be where we collect our final answer.

### 7. Collect the Top K Frequent Numbers

```python
for i in range(len(freq) - 1, 0, -1):
    for n in freq[i]:
        res.append(n)
        if len(res) == k:
            return res
```

- `for i in range(len(freq) - 1, 0, -1):` This loop goes through the `freq` list backwards, starting from the end (largest bucket) and going to the start (smallest bucket).
  - `len(freq) - 1:` This gives the index of the last bucket. Since `len(freq) = 9`, `len(freq) - 1 = 8`.
  - `0, -1:` This means we go from the last bucket to the first bucket, but we don't include bucket 0.

### Detailed Iterations:

1. **i = 8:** (Empty bucket, so skip)
2. **i = 7:** (Empty bucket, so skip)
3. **i = 6:** (Empty bucket, so skip)
4. **i = 5:** (Empty bucket, so skip)
5. **i = 4:** (Empty bucket, so skip)
6. **i = 3:** 
   - `freq[3]:` [2] (Number 2 appears 3 times)
   - `for n in freq[i]:`
     - `n = 2:` 
       - `res.append(2):` Add 2 to the result list.
       - `res = [2]`
       - `if len(res) == k:` `len(res) = 1`, which is not equal to `k = 2`, so continue.

7. **i = 2:** 
   - `freq[2]:` [1, 3] (Numbers 1 and 3 appear 2 times)
   - `for n in freq[i]:`
     - `n = 1:` 
       - `res.append(1):` Add 1 to the result list.
       - `res = [2, 1]`
       - `if len(res) == k:` `len(res) = 2`, which is equal to `k = 2`, so return `res`.

### Final Visualization:

1. **Count Dictionary:**
   ```
   count = {1: 2, 2: 3, 3: 2, 4: 1}
   ```

2. **Frequency Buckets After Filling:**
   ```
   freq = [[], [4], [1, 3], [2], [], [], [], [], []]
   ```

3. **Result List After Collecting Top K Frequent Numbers:**
   ```
   res = [2, 1]
   ```

## Conclusion

The final result for the given example (`nums = [1, 1, 2, 2, 2, 3, 3, 4]` and `k = 2`) is `[2, 1]`, meaning the numbers 2 and 1 are the top 2 most frequent numbers in the list.

By breaking down the function and visualizing each step, we can clearly understand how the `topKFrequent` function works. This approach can be applied to other problems as well, making complex code more approachable and easier to understand.

-----
