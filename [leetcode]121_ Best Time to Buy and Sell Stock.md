# 121. Best Time to Buy and Sell Stock

**1. 과제개요**

- 최고의 수익을 낼 수 있는 매수/매도 시점에서의 수익을 구하여라

> You are given an array prices where prices[i] is the price of a given stock on the ith day.
> You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock.
> Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.

**2. 초반 풀이**

- 인덱스가 1보다 큰 부분들을 하나씩 순회하면서
- 그 부분 중 최대값과 그보다 왼쪽에 있는 원소들과의 차이를 구하면서 가장 큰 값으로 업데이트
- 완료 후 해당 최대값은 리스트에서 삭제
- 같은 과정 반복하는데, 만약 최대값이 현재 기준 최고 수익보다 작으면 거기에서 프로세스 종료

- ....괜찮은 방식이라고 생각했는데 두번 loop 하는 로직인건 마찬가지인 셈이라 타임아웃...

```python
class Solution:
    def maxProfit(self, prices):

        dupPrices = prices
        result = 0

        while len(dupPrices)>1:
            mx = max(dupPrices[1:])
            if result > mx:
                return result
            idx = prices.index(mx)
            for i in range(idx):
                if result < mx - prices[i]:
                    result = mx - prices[i]
            dupPrices.remove(mx)

        return result
```

**3. 교재 및 모범풀이**

- 맨 앞에서부터 반복하면서
- 현재기준 최소값보다 작으면 최소값 업데이트 한 뒤
- 현재 값과 최소값의 차이와 현재기준 이익 중 더 큰 값 업데이트
- 상위 하위 44.29%

```python
class Solution:
    def maxProfit(self, prices):

        profit = 0
        min_price = sys.maxsize

        for price in prices:
            min_price = min(price, min_price)
            profit = max(profit, price-min_price)

        return profit
```

**4. Takeaway**

- min값 지정할때 sys.maxsize로 지정하는 방식....이렇게 해야 뭐가 나와도 업데이트가 된다
- 한 번에 최적을 구해서 해결해나가려고 하지 말고 그때그때의 최적값을 업데이트해서 결과적으로 답이 나오게 하는 방식을 고민해보자.
