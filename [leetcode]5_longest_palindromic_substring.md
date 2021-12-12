# 5. Longest Palindromic Substring

1. 과제개요

주어진 인풋 스트링에 대해서, 가장 길이가 긴 palindromic substring을 리턴한다.

2. 초반 풀이

- Palindrome 판별하는 함수 만든 뒤 가장 긴 길이부터 탐색하기 시작하는 방식..
- 속도가 매우 느렸다. 7316 ms...

```python
class Solution:
    def longestPalindrome(self, s: str) -> str:

        def isPalindrome(a:str) -> bool:
            if a == a[::-1]:
                return True

        length = len(s)
        for i in range(length,0,-1):
            for j in range(length-i+1):
                if isPalindrome(s[j:j+i]):
                    return s[j:j+i]
```
