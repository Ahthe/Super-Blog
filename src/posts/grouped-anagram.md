---
title: 4. Group Anagrams - Arrays and Hashing
description: Group Anagrams.
date: '2024-10-8'
categories:
  - LeetCode
  - Python
published: true
---
# 4. Group Anagrams - Arrays and Hashing

## Optimzed Solution

Time Complexity: O(m.n)
Space Complexity: O(n)

```python
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        ans = defaultdict(list)
        for s in strs:
            count = [0] * 26
            for c in s:
                count[ord(c) - ord("a")] += 1
            ans[tuple(count)].append(s)
        return ans.values()
```



## Visualization with Example:

Let's say the input list of strings is:

```python
strs = ["eat", "tea", "tan", "ate", "nat", "bat"]
```

### Step-by-Step Explanation:

#### 1. Initialization of the `defaultdict`:

```python
ans = defaultdict(list)
```

`ans` is a dictionary where each key is a tuple representing the character count of a string (using a list of size 26 to represent 'a' to 'z').

Initially, `ans` is empty: 
```python
{}
```

#### 2. Processing the first string "eat":

```python
count = [0] * 26  # Initialize a count list for letters
```

We create an array `count` of size 26 to represent each letter of the alphabet ('a' to 'z'), all set to zero:

```makefile
count = [0, 0, 0, 0, ..., 0]  # 26 zeros
```

```python
for c in "eat":
    count[ord(c) - ord("a")] += 1
```

For each character in `"eat"`, we update the count array:

- `'e'` -> `count[ord('e') - ord('a')] += 1`, so `count[4] += 1` -> now, `count[4] = 1`
- `'a'` -> `count[ord('a') - ord('a')] += 1`, so `count[0] += 1` -> now, `count[0] = 1`
- `'t'` -> `count[ord('t') - ord('a')] += 1`, so `count[19] += 1` -> now, `count[19] = 1`

After processing `"eat"`, the count array looks like:

```css
count = [1, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, ..., 0]
```

We convert the `count` array into a tuple (because lists are not hashable and can't be used as keys in a dictionary):

```scss
tuple(count) = (1, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, ..., 0)
```

Now, we store `"eat"` in `ans` with this tuple as the key:

```css
ans = {(1, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, ..., 0): ["eat"]}
```

#### 3. Processing the second string "tea":

Similarly, we create the count array for `"tea"`:

- `'t'` -> `count[19] += 1`
- `'e'` -> `count[4] += 1`
- `'a'` -> `count[0] += 1`

After processing `"tea"`, the count array looks like:

```css
count = [1, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, ..., 0]
```

The tuple is the same as for `"eat"`:

```scss
tuple(count) = (1, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, ..., 0)
```

`"tea"` is added to the same key in `ans`:

```css
ans = {(1, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, ..., 0): ["eat", "tea"]}
```

#### 4. Processing the third string "tan":

After processing `"tan"`, the count array becomes:

```css
count = [1, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, ..., 0]
```

The tuple:

```scss
tuple(count) = (1, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, ..., 0)
```

Now, `"tan"` is stored in a new key in `ans`:

```less
ans = {
  (1, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, ..., 0): ["eat", "tea"],
  (1, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, ..., 0): ["tan"]
}
```

#### 5. Processing "ate", "nat", and "bat":

Each of these strings will similarly generate a count array and corresponding tuple.

- `"ate"` is grouped with `"eat"` and `"tea"`:

```less
ans = {
  (1, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, ..., 0): ["eat", "tea", "ate"],
  (1, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, ..., 0): ["tan"],
  (1, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, ..., 0): ["nat"],
  (1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, ..., 0): ["bat"]
}
```

#### 6. Returning the values:

```python
return ans.values()
```

Finally, we return the grouped anagrams as lists of lists:

```css
[["eat", "tea", "ate"], ["tan", "nat"], ["bat"]]
```

### Key Points:

- `ans[tuple(count)]`: The tuple represents the frequency of each letter in the string, and this acts as the key for grouping anagrams.
- `tuple`: Converting the list `count` to a tuple is necessary because only immutable types like tuples can be used as keys in dictionaries.
- `ans.values()`: This returns the grouped anagrams as a list of lists.
