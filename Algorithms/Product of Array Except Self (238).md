==Medium== Question [link](https://leetcode.com/problems/product-of-array-except-self/) from [[Leetcode]]

### ==**Code:**==

1) ==**T: O(N)**== and ==**S: O(N)**==
```python
class Solution:
	def productExceptSelf(self, nums: List[int]) -> List[int]:
		result = [1] * len(nums)

		prefix = 1
		for idx, num in enumerate(nums):	
			result[idx] = prefix
			prefix *= num
		
		postfix = 1
		for i in range(len(nums) - 1, -1, -1):
			result[i] *= postfix	
			postfix *= nums[i]
		
		return result
```

### ==**Explanation**==

Explanation 1 (Rus) - [link](https://www.youtube.com/watch?v=RGQ1blF6P7s)
Explanation 2 (Eng) - [link](https://www.youtube.com/watch?v=bNvIQI2wAjk)
Explanation 3 (Eng) - [link](https://www.youtube.com/watch?v=yKZFurr4GQA)

### ==Explanation on my words==
### ==*ENG*==

```
Input: nums = [1,2,3,4] 
Output: [24,12,8,6]
```

```
At index 0, 24 is consisted of 2 * 3 * 4 
At index 1, 12 is consisted of 1 * 3 * 4 
At index 2, 8 is consisted of 1 * 2 * 4 
At index 3, 6 is consisted of 1 * 2 * 3
```

⭐️ Points

Based on the example above, it seems that by looping twice, once from the left and once from the right, the calculation can be simplified. **The sum of the numbers to the left of an index can be calculated during the left-to-right loop (prefix), and the sum of the numbers to the right can be calculated during the right-to-left loop (postfix).** This way, it seems possible to perform the calculation without skipping over the current index.

Let's see how it works!

```sql
[1, 2, 3, 4]

output = [1, 1, 1, 1]
prefix = 1
```

We initialize `output` with `1` because `1` doesn't affect a result of multiplication. `left` is a total of multiplication on the left side.

* **`right-to-left`**

First of all, we run left-to-right loop and calculate `prefix`.
```python
nums = [1, 2, 3, 4]
		↑ i
result = [1, 1, 1, 1]
prefix = 1↑ updated
```

We put prefix value into `result[i]` (`i` is `0` in this situation) and multiply `nums[i]` (`i` is `0` in this situation). because index `0` is prefix of index `1`.

```python
result[i] = prefix
prefix *= nums[i]
```

Next, we still have prefix `1` because `1 * 1 = 1` but `prefix` value is `nums[0] `
```python
nums = [1, 2, 3, 4]
		   ↑ i
result = [1, 1, 1, 1]
prefix = 1
```

We put prefix value into `result[i]` (`i` is `1`) and multiply `prefix` to `nums[i]` (`1 * 1 = 1`) 

```python
result[i] = prefix
prefix *= nums[i]

nums = [1, 2, 3, 4]
Updated: result = [1, 1, 1, 1]
Updated: prefix = 2   ↑ updated
```

We have prefix `2` because `1 * 2 = 1` and `prefix` value is `nums[1]`

Next, interesting action is staring here
```python
nums = [1, 2, 3, 4]
			  ↑ i
result = [1, 1, 1, 1]
prefix = 2
```

We put prefix value into `result[i]` (`i` is `2`) and multiply `prefix` to `nums[i]` (`1 * 3 = 2`) 

> **We calculate the prefix one step earlier where this prefix is ​​valid**

```python
nums = [1, 2, 3, 4]
Updated: result = [1, 1, 2, 1]
Updated: prefix = 6      ↑ updated
```

we have prefix `6` (`2 * 3 = 1)

Next
```python
nums = [1, 2, 3, 4]
		         ↑ i
result = [1, 1, 2, 1]
prefix = 6
```

1. put prefix value into `result[i]` (`i` is `3`) 
2. multiply `prefix` to `nums[i]` (`1 * 3 = 2`) 

```python
nums = [1, 2, 3, 4]
Updated: result = [1, 1, 2, 6]
Updated: prefix = 24        ↑ updated
```

We do not need last prefix anymore.

- **`left-to-right`**

Now, let's start same procedure for `postfix`. We run `left-to-right` to calculate the `postfix`. However, We have real numbers in results instead of default `1`

```python
nums = [1, 2, 3, 4]
		         ↑ i
result = [1, 1, 2, 6]
postfix = 1
```

1. put `postfix` value into `result[i]` (`i` is `3`)
2. multiply `postfix` to `prefix` (`result[i]`) (`1 * 6 = 6`) and update `result[i]`
3. update `postfix` to `nums[i]` with multiplying

```python
result[i] *= postfix
postfix *= nums[i]

nums = [1, 2, 3, 4]
Updated: result = [1, 1, 2, 6]
Updated: postfix = 4        ↑ updated
```

Next
```python
nums = [1, 2, 3, 4]
		      ↑ i
result = [1, 1, 2, 6]
postfix = 4
```

1. put `postfix` value into `result[i]` (`i` is `2`)
2. multiply `postfix` to `result[i]` (`4 * 2 = 8`)  
3. update `postfix` to `nums[i]` with multiplying

```python
nums = [1, 2, 3, 4]
prefix = [1, 1, 2, 6]
postfix= [1, 1, 4, 1]
Updated: result = [1, 1, 8, 6]
Updated: postfix = 12    ↑ updated
```

Next
```python
nums = [1, 2, 3, 4]
		   ↑ i
result = [1, 1, 2, 6]
postfix = 12
```

1. put `postfix` value into `result[i]` (`i` is `1`)
2. multiply `postfix` to `result[i]` (`12 * 1 = 12`)  
3. update `postfix` to `nums[i]` with multiplying

```python
nums = [1, 2, 3, 4]
prefix = [1, 1, 2, 6]
postfix= [1, 12, 4, 1]
Updated: result = [1, 12, 8, 6]
Updated: postfix = 24 ↑ updated
```

Next
```python
nums = [1, 2, 3, 4]
		↑ i
result = [1, 12, 8, 6]
postfix = 24
```

1. put `postfix` value into `result[i]` (`i` is `0`)
2. multiply `postfix` to `result[i]` (`24 * 1 = 24`)  
3. update `postfix` to `nums[i]` with multiplying

```python
nums = [1, 2, 3, 4]
prefix = [1, 1, 2, 6]
postfix= [24, 12, 4, 1]
Updated: result = [24, 12, 8, 6]
			       ↑ updated
Updated: postfix = 24
```

We do not need last `postfix` anymore.


At the end We just need to return `result`


![[Product of Array Except Self 1.png]]

![[Product of Array Except Self 2.png]]

![[Product of Array Except Self 3.png]]
