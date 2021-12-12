# 5. Longest Palindromic Substring

1. 과제개요

- 주어진 인풋 스트링에 대해서, 가장 길이가 긴 palindromic substring을 리턴한다.

2. 초반 풀이

- Palindrome 판별하는 함수 만든 뒤 가장 긴 길이부터 탐색하기 시작하는 방식..~~사실 굳이 함수가 필요없긴 하다..~~
- 7316 ms...

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

3. 교재 및 모범풀이

- 인풋 string 앞에서부터 차례대로
- 홀수, 짝수인 경우 나눠서 (p1, p2) get_palindrome 함수로 palindrome 구함
- 그리고 가장 길이가 긴 p값을 계속 갱신해나감 (최종적으로 가장 길이가 긴 p가 남게 됨)
- get_palindrome 지정된 두 범위에서부터 오른쪽, 왼쪽으로 한칸씩 늘려가며 특정 조건을 만족할때까지만 반복하는 방식
- 976 ms

```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        p = ''
        for i in range(len(s)):
            p1 = self.get_palindrome(s, i, i+1)
            p2 = self.get_palindrome(s, i, i)
            p = max([p, p1, p2], key=lambda x: len(x))
        return p

    def get_palindrome(self, s: str, l: int, r: int) -> str:
        while l >= 0 and r < len(s) and s[l] == s[r]:
            l -= 1
            r += 1
        return s[l+1:r]
```

4. Takeaway

- ㅡㅁ
