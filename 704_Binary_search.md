# 704. Binary search

**1. 과제개요**

- 주어진 리스트에서 target의 인덱스를 찾고 없으면 -1.
- 다만 복잡도는 O(logN) 으로 할 것. (전체 순회하는 것 불가하다는 뜻!)

**2. 초반 풀이**

- 중간 지점을 지정한 뒤, 해당 지점부터 target과 비교하여 왼쪽 오른쪽으로 이동
- 하위 82.88%

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:

        if target not in nums:
            return -1

        idx = int(len(nums)/2)

        if nums[idx] == target:
            return nums.index(nums[idx])

        while nums[idx] != target:
            if nums[idx] > target:
                idx -= 1
            else:
                idx += 1

        return idx
```

**3. 교재 및 모범풀이**

- 왼쪽 오른쪽 지정한 뒤에 그 구간 안에 있는 중심점 찾은 뒤
- 그 중심점 기준으로 target과 비교 후 전체 범위를 재설정
- 과정을 반복하여 답 구함

- 실제로 실행횟수도 더 적을 것 같고 -1 따로처리할 필요 없어서 더 효과적일 것 같은데
- 하위 82.88%... 소요된 시간은 똑같다..

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:

        left, right = 0, len(nums)-1

        while left <= right:

            pivot = left + (right-left) // 2

            if nums[pivot] == target:
                return pivot
            if nums[pivot] < target:
                left = pivot + 1
            else:
                right = pivot - 1

        return -1
```

**4. Takeaway**

- binary search의 전형적인 문제
