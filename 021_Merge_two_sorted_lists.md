# 21. Merge_two_sorted_lists

**1. 과제개요**

- 정렬되어 있는 두 개의 연결 리스트를 합쳐라
  > You are given the heads of two sorted linked lists list1 and list2.
  > Merge the two lists in a one sorted list. The list should be made by splicing together the nodes of the first two lists.
  > Return the head of the merged linked list.

**2. 초반 풀이**

- 둘 다 리스트로 변경한 뒤 리스트를 정렬하고 그걸 다시 연결리스트로 변경하는 방식..
- 하위 76.75%. 썩 나쁘진 않다. 다만 코드는 좀 지저분...

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:

        lst1 = []
        lst2 = []

        current_list1 = list1
        current_list2 = list2

        if current_list1 is None:
            lst1 = []
        else:
            lst1.append(current_list1.val)
            while current_list1.next is not None:
                current_list1 = current_list1.next
                lst1.append(current_list1.val)

        if current_list2 is None:
            lst2 = []
        else:
            lst2.append(current_list2.val)
            while current_list2.next is not None:
                current_list2 = current_list2.next
                lst2.append(current_list2.val)

        lst = lst1 + lst2
        if lst == []:
            return ListNode(val='')

        lst.sort()

        result = ListNode(lst[0])
        tail = result
        i = 1
        while i < len(lst):
            tail.next = ListNode(lst[i])
            tail = tail.next
            i += 1

        return result
```

**3. 교재 및 모범풀이**

- 리스트로 변경하지 않고 값을 구하는 방식
- 값을 하나씩 까보면서 업데이트 후 next 처리해주는 방식..
- 두 값 비교하면서 하나씩 업데이트하다가 한쪽이 없어지면 다른쪽을 뒤에 넣어준다.

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def mergeTwoLists(self, l1, l2):
        dummy = cur = ListNode(0)
        while l1 and l2:
            if l1.val < l2.val:
                cur.next = l1
                l1 = l1.next
            else:
                cur.next = l2
                l2 = l2.next
            cur = cur.next
        cur.next = l1 or l2
        return dummy.next
```

**4. Takeaway**
