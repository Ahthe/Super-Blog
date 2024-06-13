---
title: Leet Code Series 2
description: Merge Two Sorted List.
date: '2024-5-9'
categories:
  - LeetCode
  - Java
  - Python
published: true
---

## Problems List

- [Merge Two Sorted Linked Lists](#merge-two-sorted-linked-lists) 

### Merge Two Sorted Linked Lists

[Link to the Problem](https://leetcode.com/problems/merge-two-sorted-lists/submissions/1253113440/)

You are given the heads of two sorted linked lists `list1` and `list2`.

Merge the two lists in a one sorted list. The list should be made by splicing together the nodes of the first two lists.
Return the head of the merged linked list.

**Solution in Python**
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def mergeTwoLists(self, list1: ListNode, list2: ListNode) -> ListNode:
        dummy = node = ListNode()

        while list1 and list2:
            if list1.val < list2.val:
                node.next = list1
                list1 = list1.next
            else:
                node.next = list2
                list2 = list2.next
            node = node.next

        node.next = list1 or list2

        return dummy.next
```
*Time Complexity = O(n)* <br/>
*Space Complexity = O(1)*


**Explanation**

1.We create a dummy `node` and a pointer `node` to keep track of the merged list. 
```python
 dummy = node = ListNode()
```
2. We iterate through both lists using a while loop until one of them becomes empty.
```python
while list1 and list2:
``` 
3. Inside the loop, we compare the values of the current nodes of both lists. We append the node with the smaller value to the merged list and move the pointer of that list to the next node.
```python
 if list1.val < list2.val:
    node.next = list1
    list1 = list1.next
else:
    node.next = list2
    list2 = list2.next
```      
4. After appending the node, we move the `node` pointer to the newly added node.
```python
node = node.next
```      
5. Once one of the lists becomes empty, we append the remaining nodes of the other list to the merged list.
```python
node.next = list1 or list2
``` 
This line effectively appends the remaining nodes because `list1` or `list2` will be `None` for the empty list, and the non-empty list will be assigned to `node.next`. 
<br/>

6. Finally, we return dummy.next, which represents the head of the merged list. We skip the dummy node since it was used only for initialization purposes.
```python
return dummy.next
```

**Solution in Java**

```java
  class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        // Okay, here we go. First, we need to create a dummy node.
        ListNode returnNode = new ListNode(Integer.MIN_VALUE);
        // We create a headNode to keep track of the start of the merged list.
        // This is necessary because returnNode will move as we build the merged list.
        ListNode headNode = returnNode;

        // Here is the main concept of how it is going to work:
        // We use a while loop to check if both l1 and l2 are not empty.
        while (l1 != null && l2 != null) {
            // We traverse through the lists until one of them reaches the end.
            if (l1.val <= l2.val) {
                returnNode.next = l1;
                l1 = l1.next;
            } else {
                returnNode.next = l2;
                // We need to move the pointer to the next value.
                l2 = l2.next;
            }
            // Move the returnNode pointer to the next node.
            returnNode = returnNode.next;
        }

        // Now, we need to append the remaining list.
        if (l1 == null) {
            returnNode.next = l2;
        } else if (l2 == null) {
            returnNode.next = l1;
        }

        // We return headNode.next because headNode is the dummy node we created at the beginning.
        // The actual merged list starts from the next node of headNode.
        return headNode.next;
    }
  }
```

I also wanted to share another way of solving this problem by using recursion

```java
 public ListNode mergeTwoLists(ListNode l1, ListNode l2){
		if(l1 == null) return l2;
		if(l2 == null) return l1;
		if(l1.val < l2.val){
			l1.next = mergeTwoLists(l1.next, l2);
			return l1;
		} else{
			l2.next = mergeTwoLists(l1, l2.next);
			return l2;
		}
  }
```
-----
