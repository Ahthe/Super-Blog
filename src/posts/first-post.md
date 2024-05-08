---
title: Leet Code Series 1
description: First post.
date: '2024-5-8'
categories:
  - LeetCode
  - Java
  - Python
published: true
---

## Problems List

- [Two Sum](#two-sum)
- [Valid Parentheses](#valid-parentheses)

### Two Sum
[Link to the Problem](https://leetcode.com/problems/two-sum/description/)

Imagine you're given an array of integers and a target sum. Your task is to find two numbers in the array that add up to the target sum. Sounds simple, right? Well, it's not as easy as it seems!

Let's take a look at an example:

nums = [2, 7, 11, 15], target = 9

In this case, the two numbers that add up to 9 are 2 and 7. But how do we find them efficiently?

The efficient way is to use a hash map to store the values and their indices. We can iterate through the array once and add each value to the hash map. For each value, we check if the difference between the target and the value exists in the hash map. If it does, we return the indices of the two values

**Solution in Python**
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        prevMap = {}  # val -> index

        for i, n in enumerate(nums):
            diff = target - n
            if diff in prevMap:
                return [prevMap[diff], i]
            prevMap[n] = i
```
*Time Complexity = O(n)* <br/>
*Space Complexity = O(n)*


**Explanation**
1. We create an empty hash map prevMap to store the values and their indices.

```python
     prevMap = {}  # val -> index
```    
2. We iterate through the array nums using enumerate, which gives us both the index i and the value n.
```python
   for i, n in enumerate(nums):
```
 
3. This snippet is the heart of the solution. We calculate the difference between the target sum and the current number n. <br/> <br/>
If we find a match in the prevMap dictionary, it means we've found the two numbers that add up to the target sum. We return their indices, and we're done!
```python
  diff = target - n
  if diff in prevMap:
      return [prevMap[diff], i]
```
4. If the difference diff doesn't exist in the hash map, we add the current value n to the hash map with its index i.
```python
prevMap[n] = i
```

**Solution in Java**

```java
int[] twoSumHashing(int[] nums, int target){

// Creating a HashMap
Map<Integer, Integer> map = new HashMap<>();

for(int i = 0; i < nums.length; i++){

    // Get the complement using the target value
    int complement = target - nums[i];

    // Search the hashmap for complement
    //, if found, we got our pair
    if(map.containsKey(complement)){
      return new int[]{map.get(complement), i};
    }
    // Put the element in hashmap for subsequent searches.
    map.put(nums[i], i);
  }
throw new IllegalArgumentException("No two sum solution was found");
}
```
----------------------------------------------

### Valid Parentheses

[Link to the Problem](https://leetcode.com/problems/valid-parentheses/description/)

Given a string `s` containing just the characters `(`, `)`, `[`, `]`, `{`, and `}`, determine if the input string is valid.

An input string is valid if:

* Open brackets must be closed by the same type of brackets.
* Open brackets must be closed in the correct order.

`Input: "()"`
`Output: true`

`Input: "()[]{}"`
`Output: true`

`Input: "(]"`
`Output: false`

**Solution in Python**
```python
class Solution:
    def isValid(self, s: str) -> bool:
        Map = {")" : "(", "]" : "[", "}" : "{"}
        stack = []
        for c in s:
            if c not in Map:
                stack.append(c)
                continue
            if not stack or stack[-1] != Map[c]:
                return False
            stack.pop()
        return not stack
```
*Time Complexity = O(n)* <br/>
*Space Complexity = O(n)*


**Explanation**
1. First we create a dictionary Map to map closing parentheses to their corresponding opening ones. We then initialize an empty stack to keep track of opening parentheses.
```python
 Map = {")" : "(", "]" : "[", "}" : "{"}

 stack = []
```


2. We iterate through each character in the input string. If the character is not a closing parenthesis, we push it onto the stack.
```python
  for c in s:
    if c not in Map:
       stack.append(c)
       continue
``` 
3. If the stack is empty or the top of the stack doesn't match the corresponding opening parenthesis, return False
```python
  if not stack or stack[-1]!= Map[c]:
  return False
```   
    
4. If the stack is not empty and the top of the stack matches the corresponding opening parenthesis, we pop the opening parenthesis from the stack.
```python
  stack.pop()
```   
    
5. Finally, we return True if the stack is empty at the end of the iteration, indicating all parentheses were matched correctly.
```python
  return not stack
``` 

**Solution in Java**
```java
class Solution {
  public boolean isValid(String s) {
    // create an empty stack
    Stack<Character> stack = new Stack<Character>(); 
    // loop through each character in the string
    for (char c : s.toCharArray()) { 
    // if the character is an opening parenthesis
      if (c == '(') 
    // push the corresponding closing parenthesis onto the stack
          stack.push(')');
    // if the character is an opening brace 
      else if (c == '{') 
      // push the corresponding closing brace onto the stack
          stack.push('}'); 
      // if the character is an opening bracket
      else if (c == '[')
      // push the corresponding closing bracket onto the stack 
          stack.push(']'); 
      // if the character is a closing bracket
      else if (stack.isEmpty() || stack.pop() != c)           
      // if the stack is empty (i.e., there is no matching opening bracket) or the top of the stack         
      // does not match the closing bracket, the string is not valid, so return false           
      return false;
    }
        // if the stack is empty, all opening brackets have been matched with their corresponding closing brackets,
        // so the string is valid, otherwise, there are unmatched opening brackets, so return false
        return stack.isEmpty();
    }
}

```
*Time Complexity = O(n)* <br/>
*Space Complexity = O(n)*

Thank You for reading, Have a nice day! <br/>

-Ahthesham `😁`


### References
- [NeetCode](https://neetcode.io/practice)
- [StudyAlgorithms](https://studyalgorithms.com/array/leetcode-two-sum/)
