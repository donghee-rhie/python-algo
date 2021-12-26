# 206. Reversed Linked List

**1. 과제개요**

- 연결 리스트를 뒤집어라
  > Given the head of a singly linked list, reverse the list, and return the reversed list.

**2. 초반 풀이**

- 인풋을 리스트로 변경한 뒤 뒤집고 Linked List로 변환
- 하위 87.34%...

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:

        lst = []
        current = head
        while current is not None:
            lst.append(current.val)
            current = current.next

        lst = lst[::-1]

        if len(lst) == 0:
            return ListNode(val='', next=None)

        tmp = result = ListNode()
        tmp.val = lst[0]
        i = 1
        while i < len(lst):
            tmp.next = ListNode(lst[i])
            tmp = tmp.next
            i += 1

        return result
```

**3. 교재 및 모범풀이**

-
- 하위 87.34%..

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseList(self, head):
        prev = None
        curr = head

        while curr:
            next = curr.next
            curr.next = prev
            prev = curr
            curr = next

        return prev
```

**4. Takeaway**
