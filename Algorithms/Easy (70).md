Climbing Stairs Question [link](https://leetcode.com/problems/climbing-stairs/) from [[Leetcode]]

### ==**Code:**==

1) ==**O(N)**== (simple to understand)
```python
if n < 3:  
    return n  
  
sts = [1, 2]  
for i in range(2, n):  
    sts.append(sts[i-2] + sts[i-1])  
return sts[-1]
```

2)  ==**O(N)==
```python
if n < 3:  
    return n  
  
st1, st2 = 1, 2  
for _ in range(n - 2):  
    st1, st2 = st2, st2 + st1  
return st2
```

3) ==**O(N)**==
```python
step = {1: 1, 2: 2}  
def climbStairs(self, n: int) -> int:  
    if n in self.step:  
        return self.step[n]  
    self.step[n] = self.climbStairs(n - 1) + self.climbStairs(n - 2)  
    return self.step[n]
```

### ==**Explanation**==

Explanation 1 (Rus) - [link](https://www.youtube.com/watch?v=u43aQ4Vgvs0  )
Explanation 2 (Eng) - [link](https://www.youtube.com/shorts/UY6d4cv-0RI)

### ==**Definition in UZB**==

Bza barcha qadamlarni saqlab yurshimiz shart emas. Biza 1 ta zinapoyalar (stairs) ga va 2 taga chiqishni bilamiza. Demak `n[i]` ga chiqishga ketadigan kombinatsiyalar yeg'indisini, o'zidan 1 ta va 2ta oldingi zinapoyalar (stairs) chiqishga ketadigan kombinatsiyalar yeg'indisini orqali bilvosi boldi.
Masalan: 
* 1 ga - ==1== ta kombinatsiya bor
* 2 ga - ==2== ta kombinatsiya bor
* 3 ga - 2 `n[i - 1]` ga 1ta qadam qoshsak 3ga chiqamiza va 1ga `n[i - 2]` 2 tali qadam. -> 2 da 2ta kombinatsiyalar boridi 1 da esa 1 ta -> 2 + 1 = ==3==
* 4 ga - 3 `n[i - 1]` ga 1 ta qadam qoshamiza va 2 `n[i - 2]` ga 2tali qadamdan 1ta qadam. -> 3 `n[i - 1]` ga chiqish uchun 3ta kombinatsiyalar, 2 `n[i - 2]` ga chiqish uchun 2 ta kombinatsiyalar -> 3 + 2 = ==5==

**Fibonacci** uchun standard sovol va **Recursiya** ishlatish uchun ham. 
![[Untitled.jpg]]

### ==**Definition in ENG**==

We may not save all out stairs combinations (distinct ways to climb to the top) or steps. We know the 1st and 2nd stairs in advance. That means we can figure out combinations for `n[i]` by adding  1 `n[i - 1]` and 2 `n[i - 2]` front stairs because they also save the value of the combinations (values/climbs) before themselves.
For example:
* 1 - there is ==1== combination
* 2 - there are ==2== combinations
* 3 - We can climb to the top with 1 climb from 2nd position and with 2 climbs from 1st position. We add value of 2nd `n[i - 1]` stair to 1st `n[i - 2]` to get value for 3rd stair (do you remember what we said above ? every climbs save the value of combinations before themselves.) -> We had 2 climbs (combinations) on 2 and 1 on 1 -> 2 + 1 = ==3==
* 4 - We can reach the 4th climb from 3rd `n[i - 1]` by adding 1 climb or from 2nd `n[i - 2]` by adding 2 climbs  -> We calculated 3 climbs (combinations) as result to reach the 3rd  `n[i - 1]` position and calculated 2 climbs (combinations) as result to reach the 2nd `n[i - 2]` position -> 3 + 2 = ==5== 

Default problem to solve using **Fibonacci** and using **Recursion**
![[leetcode ez 70 1.jpg]]

