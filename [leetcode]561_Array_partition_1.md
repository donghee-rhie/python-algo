# 561. Array partition 1

**1. 과제개요**

- 짝수개의 원소로 구성된 주어진 리스트에 대해서
- 원소를 두개씩 짝지은 뒤
- 그룹별로 최소값을 더한 값의 최대값을 찾아라...

> > Given an integer array nums of 2n integers, group these integers into n pairs (a1, b1), (a2, b2), ..., (an, bn) such that the sum of min(ai, bi) for all i is maximized. Return the maximized sum.

**2. 초반 풀이**

- 크기 순서대로 정렬한 뒤, 앞에서부터 2개씩 짝지워서 최소값 가지고 와서 더하면 된다.
- 하위 94.78%

```python
class Solution:
    def arrayPairSum(self, nums: List[int]) -> int:
        nums.sort()
        r = 0
        for i in range(0,len(nums),2):
            r += min(nums[i], nums[i+1])

        return r
```

**3. 교재 및 모범풀이**

- 생각해보니 정렬한 뒤 순서대로 찍짓는건데 최소값 더할 것 없이 조합 중 짝수 인덱스가 무조건 최소값이다...!
- 불필요한 loop 없애서 속도 개선
- 하위 98.02%

```python
class Solution:
    def arrayPairSum(self, nums: List[int]) -> int:
        return sum(sorted(nums)[::2])
```

**4. Takeaway**

- 불필요한 프로세스 없는지 항상 점검해볼 것
