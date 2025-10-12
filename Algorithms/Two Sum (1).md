==EASY== Two Sum Question [link](https://leetcode.com/problems/two-sum/) from [[Leetcode]]

### ==**Code:**==

1) ==**O(N)**== 
```python
pair_idx = {}  
  
for idx, val in enumerate(nums):  
    if target - val in pair_idx:  
        return [idx, pair_idx[target - val]]  
    pair_idx[val] = idx
```

2) ==O(N^2)==
```python
for i, j in enumerate(nums):  
    tmp = target - j  
    for idx in (range(i + 1, len(nums))):  
        if tmp == nums[idx]:  
            return [i, idx]
```

3) ==O(N^2)==
```python
for i in range(len(nums)):  
    a = target - nums[i]  
    a_idx = nums.index(a)  
    if a in nums and i != a_idx:  
        return [i, a_idx]
```

---
### ==**Explanation on my words**==

### ==*UZB*==
==(ID 1 Code) Tushuntirilgan. Ammo, qolgan barcha kodlarning ishlash logikasi bir xil.==

Keling birinchi kiruvchi qaymatlarni (nums, target) aniqlab olamiza.
```
Input: nums = [2, 7, 11, 15], target = 9
```

Agar biz hozirgi (`nums[i]`) qiymatni `target`'dan ayirsak bizga `target` uchun qanday son yetmiyabganini bilib olshimiz mumkin bo'ladi.

Bizda hozirgi qiymat (`nums[i]` = 2) bo'lganida, bizga `7` kerak bo'ladi `9` hosil bo'lishi uchun. Shunday qilib, agar bizda `7` raqami bo'lsa hozirgi qiymatimz (`nums[i]` = 2) bilan target (`9`)  hosil qila olamiza.
Bundan kelib chiqadiki, Biz `HashMap` ishlatshimz mumkin

> ⭐️ Asosiy joyi: Massiv'dagi qiymatni key (kalit) sifatida va uning index'sini qiymat (value) sifatida saqlaymiza.

Keling, birma-bir ko'rib chiqamiza.

```
Input: nums = [2,7,11,15], target = 9
```

`HashMap` ni biz `pair_idx` deb nomlab olamiza
```python
[2,7,11,15], target = 9
 ↑

pair_idx = {} 
```

Biz `2` raqamini topdik. Bizga `pair_idx`'dan `7` raqami kerak target (`9`) hosil qilshimiz uchun. Lekin hozir bizning `pair_idx`'da hech narsa yo'qligi uchun biz hozirgi qiymatni qoshib ketamiza.

```python
pair_idx = {2: 0} 

Hozirgi qiymat: 2
2 ning indexsi: 0
```

Keyingi qadam

```python
[2,7,11,15], target = 9
　 ↑

pair_idx = {2: 0}
```

We found `7`, so we need `2`. Check if we have `2` in `pair_idx`. And yes we have `2`.
Biz `7` raqamini topdik, endi bizga `pair_idx`'dan `2` raqami kerak target (`9`) hosil qilshimiz uchun va bizning `pair_idx` da `2` raqami mavjud (Chunki bundan oldingi raqami `2` topib uni qoshib qo'ygan edik).

```python
return [0,1] or [1,0]
```

Sovolda "Javobni istalgan tartibda qaytarishingiz mumkin" deb aytilgan.

Biz javobni topib bo'ldik ammo kelin yana davom etirib ko'ramiza

```python
pair_idx = {2: 0, 7: 1}
[2,7,11,15], target = 9
　　  ↑

Bizga kerak 9 - 11 = -2, lekin -2 pair_idx da yoq, demak
pair_idx = {2: 0, 7: 1, 11: 2}
```

```python
pair_idx = {2: 0, 7: 1, 11: 2}
[2,7,11,15], target = 9
　　     ↑

Bizga kerak 9 - 15 = -6, lekin -6 pair_idx da yoq, demak
pair_idx = {2: 0, 7: 1, 11: 2, 15: 3}
```

### ==*ENG*==
==Explanation (Code with ID 1). But other solutions works on same logic. ==

Let's take a look at input array and target number.

```
Input: nums = [2, 7, 11, 15], target = 9
```

In this case, if we subtract current number in input array from target number, we can get a number we need to create the target number.

`7` is a number we need when current number is `2`. So if we have `7` and index number of `7`, we can create `9` with the current(= `2`) number and `7`.

From this example, what we should keep in `HashMap` is

> ⭐️ *Key Points:* Keep numbers(elements) as keys and index numbers as values in the input array.

Let's iterate through one by one.

```
Input: nums = [2,7,11,15], target = 9
```

Let's call the `HashMap` `pair_idx`.

```python
[2,7,11,15], target = 9
 ↑

pair_idx = {} 
```

We found `2`. we need `7` to create `9`, so check if we have `7` in `pair_idx`. But now `pair_idx` is empty, so just add current number and its index to `pair_idx`.

```python
pair_idx = {2: 0} 

2 is current number
0 is index of 2
```

Then move next.

```python
[2,7,11,15], target = 9
　 ↑

pair_idx = {2: 0}
```

We found `7`, so we need `2`. Check if we have `2` in `pair_idx`. And yes we have `2`.

```python
return [0,1] or [1,0]
```

The description says "You can return the answer in any order".

We already found the answer but if we continue that

```python
pair_idx = {2: 0, 7: 1}
[2,7,11,15], target = 9
　　  ↑

We need 9 - 11 = -2 but no -2 in pair_idx, so
pair_idx = {2: 0, 7: 1, 11: 2}
```

```python
pair_idx = {2: 0, 7: 1, 11: 2}
[2,7,11,15], target = 9
　　     ↑

We need 9 - 15 = -6 but no -6 in pair_idx, so
pair_idx = {2: 0, 7: 1, 11: 2, 15: 3}
```