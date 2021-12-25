# 234. Palindrome Linked List

**1. 과제개요**

- 연결 리스트가 팰린드롬 구조인지 판별할 것
  > Given the head of a singly linked list, return true if it is a palindrome.

**2. 초반 풀이**

- linked list를 list로 변경한 뒤 팰린드롬 구조인지 확인하는 방법
- current_node = head로 지정해두면 current_node를 next로 보내도 head는 원래 데이터 그대로 유지된다는 점..
- 하위 65.95% 정도..

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def isPalindrome(self, head: Optional[ListNode]) -> bool:

        # node를 list로 변환하고
        lst = []
        current_node = head

        while current_node is not None:
            lst.append(current_node.val)
            current_node = current_node.next

        # 판별하기

        return lst == lst[::-1]
```

**3. 교재 및 모범풀이**

- 크게 다르지 않다...
- 팰린드롬 판별하는 방식에만 차이가 있다.
- 근데 훨씬 느리다. 하위 5% 정도...;;
- 팰린드롬 판별하는 로직이 복잡도가 더 크다.

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def isPalindrome(self, head: Optional[ListNode]) -> bool:

        # node를 list로 변환하고
        lst = []
        current_node = head

        while current_node is not None:
            lst.append(current_node.val)
            current_node = current_node.next

        # 판별하기

        while len(lst)>1:
            if lst.pop(0) != lst.pop():
                return False

        return True
```

**3-2. 교재 및 모범풀이**

- 파이썬 list는 동적 배열(?)로 구성되어 있어서 맨 앞 값을 불러오면 모든 값이 한 칸씩 시프팅 되면서 시간복잡도 O(n) 발생
- list 대신 deque 데이터타입 활용
- 이중 연결리스트 구조로 양쪽 방향 모두 추출하는데 시간복잡도 O(1)에 실행됨
- 하위 49.14%....
- 로직은 그대로고 리스트를 데크로만 바꿨을 뿐인데도 꽤 빠르다.

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def isPalindrome(self, head: Optional[ListNode]) -> bool:

        # node를 list로 변환하고
        dq = collections.deque()
        current_node = head

        while current_node is not None:
            dq.append(current_node.val)
            current_node = current_node.next

        # 판별하기

        while len(dq)>1:
            if dq.popleft() != dq.pop():
                return False

        return True
```

**4. Takeaway**

- 데크라는 자료구조 주목...
  > https://leonkong.cc/posts/python-deque.html
- 특히 push / pop이 빈번한 로직을 짤 때에는 deque를 이용하는 것 만으로도 훨씬 빨라질 수 있다.
