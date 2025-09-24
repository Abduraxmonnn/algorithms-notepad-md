"Best Time to Buy and Sell Stock" Question [link](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/description/?envType=problem-list-v2&envId=dynamic-programming) from [[Leetcode]]

### ==**Code:**==

1) ==O(N)==

  ```python
class Solution:
	def maxProfit(self, prices: List[int]) -> int:
		buy_price = prices[0] 
		profit = 0

		for i in range(len(prices)):  # <-- runs through prices list
			if prices[i] < buy_price:  # <-- smallest but_price
				buy_price = prices[i]
			else:  # current price smallest than current, to reach more profit
				tmp_profit = prices[i] - buy_price  # potential profitable deal
				if tmp_profit > profit:
				profit = tmp_profit  # <-- update if tmp more profitable

		return profit
  ```

### ==**Definition in UZB:**==

2ta o'zgaruvchi yaratib olamiza
1. ==`buy_price`==: Bu bzani sotib oladigan narx bo'ladi
2. ==`profit`==: Bu bzani foydamizani (buy - sell prices) ni saqlidi

Keyin `for n` qb chiqamiz agar `price[n] < buy` bo'sa unda `buy_price` `price[n]` ga o'zgaradi. Bo'masa yengi `profit` larni solishtiramiza

```python
tmp_profit = price[n] - buy_price
if profit > tmp_profit
```
agar shu `True` bo'lsa unda bza hozirgi profit obkevokan bitim (position/deal) dan yaxshirogini topdik va koproq foyda olamiza degani shuning uchun biza o'zimizning profitni yengisiga yenglimiza
```python
profit = tmp_profit
```

### ==**Definition in ENG:**==

We create 2 variables
1. ==`buy_price`==: Save our buy price (On what price we gonna buy)
2. ==`profit`==: Save our profit (diff: buy price - sell price)

We use `for n` If `price[n] < buy` then we will update `buy_price` to `price[n]` to keep our smallest buy price to reach a profitable deal. Otherwise, We compare current profit with new possible more profit price:
```python
tmp_profit = price[n] - buy_price
if profit > tmp_profit
```
If the if condition will be `True`, we find out the better profitable deal to update our current profit value to new one which means we need to update current profit value to new one using:
```python
profit = tmp_profit
```
We update profit throughout prices list. If we find out better deal using `price[n] - buy_price` (`tmp_price`)

### ==Other Code==:

1) ==O(N)==

```python
class Solution(object):
	def maxProfit(self, prices): 
		min_price = prices[0] 
		max_profit = 0 
	
		for i in range(1, len(prices)):
			min_price = min(min_price, prices[i])
			max_profit = max(max_profit, prices[i] - min_price)
		
		return max_profit
```
