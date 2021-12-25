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
- loop이 두개 돌지만 어쨌거나 loop안에서 in 으로 탐색하는건 마찬가지라서 시간복잡도는 위와 유사하지만 in 연산이 훨씬 가볍기 때문에 시간이 조금 걸림
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
- 다만 loop 안에서 in으로 탐색하는 부분을 없애고 딕셔너리를 활용해 해시테이블을 만들어서 조회 속도를 빠르게 만든다.
- 해시테이블 탐색의 복잡도는 대략 O(1) 수준에서 가능하므로 시간이 훨씬 단축된다.
- 56 ms..

- dict 다 만든 뒤 찾는 버전

```python
class Solution:
    def twoSum(self, nums, target):
        values = {}
        for i, num in enumerate(nums):
            values[num] = i

        for i, num in enumerate(nums):
            remaining = target - num
            if remaining in values and i != values[remaining]:
                return [i, values[remaining]]
```

- dict 다 안 만들고 처리하는 버전. 조금더 효율적이지만 탐색시간은 비슷..

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
- 딕셔너리 활용한 key/value 저장해두는 방식 적극적으로 활용하기.
