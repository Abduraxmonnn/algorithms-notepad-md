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

#### ==*Formula*==
$$
dp[i] = \max(dp[i - 1], \; nums[i] + dp[i - 2])
$$

### ==*UZB*==
Biza 2ta pointer yaratamiza `last element` va `before last element` (yoki `last element - 1`) saqlash uchun. Faqat shu 2ta qiymatga asoslanib ish qilamza. 

---
Biza 2xil yo'l bilan uylarni o'g'irlashni boshlab olshimiz mumkin:
![[Pasted image 20250928155448.png]]
1) List'dagi 1-elementdan boshlimza, 2-element ignore qilib (chunki o'g'irlomimza) undan keyingi barcha uylarni o'g'irlashimiza mumkin (ko'k rang)
	dp = [1, ~~2~~, 3, 1, 3, 4]
2) Yoki List'dagi 1-elementni ignore qilib 2-element va undan keyingi barcha uylarni  o'g'irlashimza mumkin (yashil rang)
	dp = [~~1~~, 2, 3, 1, 3, 4]


---
Biza "bu uyni ogirlimizmi yoki yoq" sovoliga asoslanib har bir uyni aylanib chiqamiza!
Boshida bizada 2ta ozgaruvchi va ikkalasida 0 qiymat boladi, bullar bizani `pointer`'larimiza, chunki biza hali hech qaysi uyni o'g'irlamadik.
init dp: `dp = [5, 3, 10, 10, 15, 7, 20]

2ta o'zgaruvchilar bilan hosil bo'lgan list (ikkita 0 larni ignore qilib yugirishi boshlimiza) -> `dp = [0, 0, 5, 3, 10, 10, 15, 7, 20]`

==`1-tekshirish`== --> Biza  0 `dp[i-1]` qiymatga ega uyni o'g'irlaymizmi yoki 5 + 0 `dp[i-2] + dp[i]` qiymatli ? 
	Albatta ==5 + 0== `dp[i-2] + dp[i]`
- updated: `dp = [0, 0, ^5, 3, 10, 10, 15, 7, 20]`

> Kotta qiymatni (o'g'irlaydigan uyimiz qiymatini) `dp[i]` ga qoyib ketamiza, shunda ohirida `list` dagi ohirgi qiymat bizning javob boladi

==`2-tekshirish`== --> Biza  0 `dp[i-1]` qiymatga ega uyni o'g'irlaymizmi yoki 5 + 0 `dp[i-2] + dp[i]` qiymatli ?
	Albatta ==5 + 0== `dp[i-2] + dp[i]`
- updated: `dp = [0, 0, 5, ^5, 10, 10, 15, 7, 20]`

==`3-tekshirish`== --> Biza  5 `dp[i-1]` qiymatga ega uyni o'g'irlaymizmi yoki 10 + 5 `dp[i-2] + dp[i]` qiymatli ? 
	Albatta ==10 + 5== `dp[i-2] + dp[i]`
* updated: `dp = [0, 0, 5, 5, ^15, 10, 15, 7, 20]`

==`4-tekshirish`== --> Biza  15 `dp[i-1]` qiymatga ega uyni o'g'irlaymizmi yoki 10 + 5 `dp[i-2] + dp[i]` qiymatli ? 
	Agar teng bo'lib qolsa farqi yoq qoyib keturamiza, barbir aynan qaysi biri o'g'irlashga foydali bolishi kelejeda bilib olamiza!
* updated: `dp = [0, 0, 5, 5, 15, ^15, 15, 7, 20]`

==`5-tekshirish`== --> Biza  15 `dp[i-1]` qiymatga ega uyni o'g'irlaymizmi yoki 15 + 15 `dp[i-2] + dp[i]` qiymatli ? 
	Albatta ==15 + 15== `dp[i-2] + dp[i]`
* updated: `dp = [0, 0, 5, 5, 15, 15, ^30, 7, 20]`

Va hakozo...

> Aslida hammasidayam tepadaka `[0, 0, 5, 5, 15, 15]` bita qiymatadan 2tadan bolmaydi, shunchaki shu misolda shunday bo'lib qoldi.

### ==*ENG*==



![[PXL_20250927_100837057 1.jpg]]

[^1]: 
