# 238. product_of_array_except_self

**1. 과제개요**

- 리스트로 주어진 인풋에 대해서, 본인을 제외한 다른 수의 곱을 리스트로 담아서 리턴해라..
- 다만 복잡도는 O(n)이어야 하며 나눗셈은 못 한다!

> Given an integer array nums, return an array answer such that answer[i] is equal to the product of all the elements of nums except nums[i].
>
> > The product of any prefix or suffix of nums is guaranteed to fit in a 32-bit integer.
> > You must write an algorithm that runs in O(n) time and without using the division operation.

**2. 초반 풀이**

- reduce를 활용한 처리 방법.
- 18/20개의 케이스를 통과하고 이후 케이스 통과실패 타임아웃...

```python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:

        result = []
        for e in nums:
            lst = nums.copy()
            lst.remove(e)
            result.append(reduce(lambda x,y:x*y, lst))

        return result
```

**3. 교재 및 모범풀이**

- 앞에서부터 하나씩 곱한 결과와, 뒤에서부터 하나씩 곱한 결과를 곱하면 된다...!
- 위 발상을 해 내는게 중요했음
- 구현 자체는 어렵지 않음...

```python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:

        out = []
        p = 1
        for i in range(0, len(nums)):
            out.append(p)
            p = p * nums[i]

        p = 1
        for i in range(len(nums)-1, -1, -1):
            out[i] = out[i] * p
            p = p * nums[i]

        return out
```

**4. Takeaway**

- 생략..
