House Robber Question [link](https://leetcode.com/problems/house-robber/) from [[Leetcode]]

### ==**Code:**==

1) ==**O(N)**== (simple to understand)
```python
before_prev, prev = 0, 0  
for i in range(len(nums)):  
    pick = nums[i] + before_prev  
    notpick = prev  
  
    curr = max(pick, notpick)  
    before_prev = prev  
    prev = curr  
  
return prev
```

2)  ==**O(N)==
```python
if len(nums) == 0: return 0  
if len(nums) == 1: return nums[0]  
if len(nums) == 2: return max(nums)  
  
# dynamic programming - decide each problem by its sub-problems:  
dp = [0] * len(nums)  
dp[0] = nums[0]  
dp[1] = max(nums[0], nums[1])  
for i in range(2, len(nums)):  
    dp[i] = max(dp[i - 1], nums[i] + dp[i - 2])  
  
return dp[-1]
```

### ==**Explanation**==

Explanation 1 (Rus) - [link](https://www.youtube.com/watch?v=br-LlFfhHbQ)
Explanation 2 (Eng) - [link](https://www.youtube.com/watch?v=kIII1uT6F8Y)
Explanation 3 (Eng) - [link](https://www.youtube.com/watch?v=73r3KWiEvyk)

### ==Explanation on my words==

![[house robber leetcode.jpg]] 
![[PXL_20250927_100837057.jpg]]

