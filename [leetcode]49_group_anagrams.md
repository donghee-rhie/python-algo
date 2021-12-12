# 49. Group Anagrams

**1. 과제개요**

- 주어진 단어들의 리스트에 대하여 Anagrams (문자 구성이 동일한 단어들) 의 그룹을 리스트로 반환하는 문제

**2. 초반 풀이**

- 진짜 말 그대로 다 풀어서 풀이한 방식...
- ...시간 초과하여 케이스를 통과하지 못했다...

```python
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:

        if len(strs) == 0:
            return [[]]

        if len(strs) == 1:
            return [[r] for r in strs]

        r = []
        for i in range(len(strs)):
            tmp = []
            for j in range(i+1, len(strs)):
                if sorted(strs[i]) == sorted(strs[j]):
                    tmp.append(i)
                    tmp.append(j)
            tmp = list(set(tmp))
            tmp = [strs[e] for e in tmp]

            if len(tmp) == 0:
                tmp.append(strs[i])

            if tmp not in r:
                no = 0
                for e in r:
                    if set(e).intersection(set(tmp)) == set(tmp) or set(e).intersection(set(tmp)) == set(e):
                        no += 1
                if no == 0:
                    r.append(tmp)
        return r
```

**3. 교재 및 모범풀이**

- 딕셔너리 데이터타입을 생각했어야 했다.
- 동일한 문자 조합의 단어들을 하나의 key의 value에 묶어둔 다음에 최종적으로 value만 리턴하는 방식.
- 다만 일반적인 dict는 처음에 key가 없는 경우에는 에러. -> **defaultdict** 활용하여 초기값 지정 및 활용
- defaultdict(list) -> key가 없는 경우 key를 생성하고 value는 []로 만들어준다..

```python
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:

        r = defaultdict(list)

        for word in strs:
            r[''.join(sorted(word))].append(word)

        return r.values()
```

**4. Takeaway**

- 비슷한 것들끼리의 그룹을 만들어 줄 때 딕셔너리 타입을 적극적으로 활용하자..
- defaultdict 적극적으로 활용하자.
