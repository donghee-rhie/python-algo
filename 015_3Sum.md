# 15. 3Sum

**1. 과제개요**

- list를 인풋으로 받아서 세 숫자의 합이 0이 되는 숫자의 조합을 찾아라
- 같은 element를 두번 이용할 수는 없음.
- 중복은 포함하지 않는다.

> Given an integer array nums, return all the triplets [nums[i], nums[j], nums[k]] such that i != j, i != k, and j != k, and nums[i] + nums[j] + nums[k] ==0.
> Notice that the solution set must not contain duplicate triplets.

**2. 초반 풀이**

- brutal force는 아예 케이스도 통과 못할 것 같다...
- two pointer를 응용하는 방식
- 앞의 원소부터 순회하면서, 순회한 지점의 다음 지점부터 끝까지 two pointer로 두 지점을 지정, 순회
- 3360ms, 하위 22.21%

```python
class Solution:
    def threeSum(self, nums):

        nums.sort()
        result = []
        length = len(nums)

        for i in range(length-2):

            if i>0 and nums[i] == nums[i-1]:
                continue

            l, r = i+1, length-1
            while r > l:
                s = nums[i] + nums[l] + nums[r]
                if s == 0:
                    lst = [nums[i], nums[l], nums[r]]
                    lst.sort()
                    if lst not in result:
                        result.append(lst)


                    r -= 1
                    l += 1
                elif s > 0:
                    r -= 1
                else:
                    l += 1

        return result
```

**3. 교재 및 모범풀이**

- 교재에서는 위의 two pointer를 활용하는 방식이 나오지만 속도가 빠르진 않은 편..
- discussion에서 찾은 더 좋은 해법.
- 앞의 원소에서 순회하고, 그 다음원소부터 또 하나씩 순회하면서 그 다음 원소에서 답이 있는지 찾는다.
- 답이 되어야 하는 숫자를 딕셔너리에 추가했다가 나중에 딕셔너리에 해당값이 있으면 add하는 방식
- 716ms, 하위 88.86%

```python
class Solution(object):
    def threeSum(self, nums):

        if len(nums) < 3:
            return []

        nums.sort()
        res = set()

        for i, v in enumerate(nums[:-2]):

            if i >= 1 and v == nums[i-1]:
                continue

            d = {}
            for x in nums[i+1:]:
                if x not in d:
                    d[-v-x] = 1
                else:
                    res.add((v, -v-x, x))

        return list(map(list, res))
```

**4. Takeaway**

- list를 활용하는 것 보다 dictionary를 활용하는 것이 시간적으로 훨씬 X 100 이득임을 확인
- 데이터 안에서 탐색을 해야하는 경우가 있는 문제는 일단 dictionary 활용 검토할 것
