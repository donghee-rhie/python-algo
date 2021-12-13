# 1. two sums

**1. 과제개요**

- 주어진 리스트 중 어떤 두개 숫자를 더하면 target의 수치가 나오는지 찾아라.
- 정답은 반드시 하나, 같은 인덱스 숫자 두개 더하면 안됨

**2. 초반 풀이**

- 부루털 포스로...두개씩 조합 다 더해보는 방식..
- 4120ms...

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        for i in range(len(nums)):
            for j in range(i+1, len(nums)):
                if nums[i] + nums[j] == target:
                    return [i, j]
```

**2-1. 다시 풀어본 풀이..**

- 리스트 element별로 하나씩 순회하면서 target과의 차이를 구한 뒤, 그 차이가 다른 원소중에 있는지 탐색하는 방식
- loop이 두개 도는 구조에서 한 번만 돌면 되는 구조로 변경..
- 832ms

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:

        for i, n in enumerate(nums):
            diff = target - n
            if diff in nums and i != nums.index(diff):
                return [i, nums.index(diff)]
```

**3. 교재 및 모범풀이**

- 전체적인 접근방식은 위와 동일함
- 다만 딕셔너리를 활용한 데이터 저장 및 호출 활용..
- 56 ms..

```python
class Solution:
    def twoSum(self, nums, target):
        values = {}
        for i, num in enumerate(nums):
            remaining = target - num
            if remaining in values:
                return [i, values[remaining]]
            else:
                values[num] = i
```

**4. Takeaway**

- brutal force 외 다른 방법 탐색해보기..
- 딕셔너리 활용한 key/value 저장해두는 방식 적극적으로 활용하기
