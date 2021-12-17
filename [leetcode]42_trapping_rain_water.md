# 42. Trapping rain water

**1. 과제개요**

- 틈 사이로 빗물이 얼마나 고이는지를 계산하는 문제...

**2. 초반 풀이**

- 층마다 가장 먼 거리 두 지점을 구한 다음에, 그 전체 면적과 fill 되어있는 면적간의 차이로 면적 구함
- ...하지만 층별로 반복하며 계산하기 때문에 층이 높아지면 엄청 많이 반복해야 함
- 그래서 318 / 320 개의 케이스를 통과했는데... 말도 안되게 긴 테스트케이스에서 시간 초과...

```python
class Solution:
    def trap(self, height: List[int]) -> int:
        # 층마다 탐색하면서
        # 그 층에 가장 거리가 먼 두 지점을 탐색하고 (만약 그 층에 포인트가 하나 이하면 종료)
        # 그 사이의 전체 면적을 구해준 뒤
        # 그 사이에 실제 차 있는 부분을 빼주고
        # 각 층별로 빼주면 된다.

        result = 0
        mxHeight = max(height)

        def getMaxDistance(i):
            l, r = 0, len(height)-1
            for j in range(len(height)):
                if height[l] < i:
                    l += 1
                if height[r] < i:
                    r -= 1
                if height[l] >=i and height[r] >=i:
                    return l, r

        for i in range(1, mxHeight+1):
            l, r = getMaxDistance(i)

            if r - l == 0:
                continue
            else:
                areaAll = r - l + 1
                areaFilled = len(list(filter(lambda x:x>=i, height)))
                area = areaAll - areaFilled
                result += area

        return result
```

**3-1. 교재 및 모범풀이\_two points**

- 관련자료
  - https://www.youtube.com/watch?v=iSjvuixMPmQ
- 제일 왼쪽과 제일 오른쪽을 두 개의 포인트로 잡고 최대 높이가 나올 때까지 안쪽으로 좁혀가며 탐색

```python
class Solution:
    def trap(self, height: List[int]) -> int:
        if not height:
            return 0

        volumn = 0
        left, right = 0, len(height) - 1
        left_max, right_max = height[left], height[right]

        while left < right:
            left_max, right_max = max(height[left], left_max), max(height[right], right_max)

            if left_max <= right_max:
                volumn += left_max - height[left]
                left += 1
            else:
                volumn += right_max - height[right]
                right -= 1

        return volumn
```

**3-2. 교재 및 모범풀이\_stack**

- stack을 업데이트하고 삭제하면서 만드는 방식
- 하아 이건 아직 잘 모르겠다...

```python
class Solution:
    def trap(self, height: List[int]) -> int:
        stack = []
        volumn = 0

        for i in range(len(height)):

            #변곡점을 만나는 경우
            while stack and height[i] > height[stack[-1]]:
                #스택에서 꺼낸다
                top = stack.pop()

                if not len(stack):
                    break

                # 이전과의 차이만큼 물 높이 처리
                distance = i - stack[-1] - 1
                waters = min(height[i], height[stack[-1]]) - height[top]

                volumn += distance * waters

            stack.append(i)

        return volumn
```

**4. Takeaway**

- 아직 확실하게 이해하지는 못한...
- 나중에 다시 한 번 읽어봐야겠다.
