==MEDIUM== Group Anagrams Question [link](https://leetcode.com/problems/group-anagrams/) from [[Leetcode]]

### ==Code:==

1) ==**O(n * m)**== (preferred)
```python
groups = defaultdict(list)  
# groups will work like:  
# act -> act -> {act: [act]}  
# cat -> act -> {act: [act, cat]}  
# tac -> act -> {act: [act, cat, tac]}  
for word in strs:  
  
    key = "".join(sorted(word))  # sorted save as list but we need str
  
    if key in groups:  
        groups[key].append(word)  
    else:  
        groups[key] = [word]  
  
return list(groups.values())
```
2) ==**O(n * m)**== (m is 26 alphabet letters)
```python
anagrams_dict = defaultdict(list)  # mapping charCount to list of Anagrams  
  
for word in strs:  
    count = [0] * 26  
    for letter in word:  
        count[ord(letter) - ord('a')] += 1  
  
    key = tuple(count)  
    anagrams_dict[key].append(word)  
  
return list(anagrams_dict.values())
```

3) ==**O(n (m log m)) = n(m log m)**==
```python
res = []  
proceed = []  
  
if strs == "":  
    return [strs]  
  
for i in range(len(strs)):  
    if strs[i] not in proceed:  
        tmp_res = [strs[i]]  
        proceed.append(strs[i])  
        for j in range(i + 1, len(strs)):  
            if Counter(strs[i]) == Counter(strs[j]):  
                tmp_res.append(strs[j])  
                proceed.append(strs[j])  
        res.append(tmp_res)  
  
return res
```

### ==**Explanation on my words**==

### ==**UZB**==
==(ID 1 Code) Tushuntirilgan. Ammo, 1 va 2 kodlarning ishlash logikasi 90% ga bir xil.==

Keling birinchi kiruvchi qaymatni (strs) aniqlab olamiza.
```
Input: strs = ["act", "pots", "tops", "cat", "stop", "hat"]
```

Agar biz `strs`'dagi barcha qiymatli sort qilib chiqsak bizning `strs` quyidagi holatga keladi

```
Sorted Input: strs = ["act", "opst", "opst", "act", "opst", "aht"]
```

Endi bu qiymatlar bilash ancha oson!

Har bir qiymatlarni sorted qilingan holatini `dict` (`groups`) da bor yoki yo'qligini tekshiramiza.

- Agar bomasa (bor) ---> O'sha kerakli key ning list tiga qoshib qo'yamiza
- Agar bomasa (yoq) ---> Hozirgi (current) qiymatga key ochib uni qiymatidagi list ga ozini qoshib qoyamiza.

> 📝 NOTE: `dict > list` ga original qiymat qoshiladi, sorted bogani shunchaki tekshirib olish uchun!

Masalan: 
```
groups: {
	act: ['act', 'cat'],
	opst: ['pots', 'tops', 'stop'],
	aht: ['hat']
} 
```
or
```python
"act"    →   "act"
"cat"    →   "act"
"pots"   →   "opst"
"tops"   →   "opst"
"stop"   →   "opst"
"hat"    →   "aht"

'act': ['act', 'cat'],
'opst': ['pots', 'tops', 'stop'],
'aht': ['hat']
```
Biz shunchaki 3 ta gruppa yaratamiza `"act"`, `"opst"` va `"aht"` 

> *Qisqa hulosa:* 
> Biza faqat har bir qiymatni sort qilib shunaqa qiymatli key bizani dictda bormi yoki yoq teshiramiza. [1] Agar bosa osha keyni qiymatiga (list) bizani original qiymati qoshamiza. [2] Bomasa yengi key yaratamiz va uning qiymatiga (list) oziniyam qoshib ketmaza, keyingi safar keganimizda osha qiymatga oxshash `anagram` osha list ga qoshiladi [1] qadamda qilingan ish qb.

Oson!😄

### ==*ENG*==
==Explanation (Code with ID 1). But 1st and 2nd solutions works on 90% same logic. ==

Let's take a look at input data.

```
Input: strs = ["act", "pots", "tops", "cat", "stop", "hat"]
```

If we sort all element of strs then our input data will be

```
Sorted Input: strs = ["act", "opst", "opst", "act", "opst", "aht"]
```

Now it's much easier to understand these values!

We check whether each sorted value exists in the `dict` (`group`) or not.

* Exists ---> Just add current value into list of dict key (list is value of key)
* Not Exists ---> Add current value in dict as new key and add itself in list (list is value of key)

> 📝 *NOTE:* dict > list` We always add original value of strs items, we use sorted value just for checking.

For example:
```
groups: {
	act: ['act', 'cat'],
	opst: ['pots', 'tops', 'stop'],
	aht: ['hat']
} 
```

Simply, if we can sort each character of each string, we can group them.

```python
"act"    →   "act"
"cat"    →   "act"
"pots"   →   "opst"
"tops"   →   "opst"
"stop"   →   "opst"
"hat"    →   "aht"

'act': ['act', 'cat'],
'opst': ['pots', 'tops', 'stop'],
'aht': ['hat']
```

We can create 3 groups with `"act"`, `"opst"` and `"aht"`.

> *Shorter Summary:*
> We just sort each element of strs and check, is this element exists in our dict (group) as a key or not. [1] If exists, we append current element to value of key (value will be list). [2] If doesn't exists, just set current element as a new key of dict (group) and append itself to the key value too (value will be list), next time If we get `anagram` string then we just repeat [1] step.

Easy!😄

---

#### Second code approach explanation (UZB)

```python
anagrams_dict = defaultdict(list)  # mapping charCount to list of Anagrams  
  
for word in strs:  
    count = [0] * 26  # 1
    for letter in word:  
        count[ord(letter) - ord('a')] += 1  # 2
  
    key = tuple(count)  # 3
    anagrams_dict[key].append(word)  # 4
  
return list(anagrams_dict.values())
```

Bu yerda bizning dict kalitimiz shunchaki str emas. Buning o'rniga biz har bir strs qiymatining hex kodidan foydalanamiz `(a...00000..c..000..t...0)`

```python
"act"    →   "act"
"cat"    →   "act"
"pots"   →   "opst"
"tops"   →   "opst"
"stop"   →   "opst"
"hat"    →   "aht"

{
    (1, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0): ['act', 'cat'],
    (0, 0x11, 0, 1, 1, 1, 0, 0, 1, 1, 0, 0x4, 0): ['pots', 'tops', 'stop'],
    (1, 0, 0x4, 0, 1, 0, 0x9, , 0, 1, 0, 0x4, 0): ['hat']
}
```

Eslatma: `0x11` yoki `0x9` bu — nechta 0 (nol) takrorlanishini bildiradi.  
Masalan: `0x4` → `0, 0, 0, 0`

Nega tuple (kortej)?
— Chunki har bir `dict` (lug‘at) kaliti o‘zgarmas (immutable) bo‘lishi kerak. `tuple` o‘zgarmas tur hisoblanadi.

1. Avval harflar uchun 0 bilan to‘ldirilgan ro‘yxat yaratiladi: `[0000 ..... n]`
2. Harflar uchun hexadecimal indeks 95, 96, 97, 98 va hokazo tarzda boshlanadi — ya’ni `A` → 95, `B` → 96, `C` → 97 va hokazo.  
    Shunday qilib, joriy harfning hex indeksidan `A` harfining indeksini ayrish orqali natija 0 dan 26 gacha bo‘lgan butun sonni beradi.  
    Bu usul 95 dan boshlashdan qochish va jarayonni soddalashtirishga yordam beradi.
3. `count` ro‘yxatini `key` (kalit) sifatida `tuple`ga aylantiramiz.
4. So‘ngra qiymatni kalitga biriktiramiz. Masalan:  
    `stop` qiymatini `(0, 0x11, 0, 1, 1, 1, 0, 0, 1, 1, 0, 0x4, 0)` ga qo‘shamiz →  
    `(0, 0x11, 0, 1, 1, 1, 0, 0, 1, 1, 0, 0x4, 0): stop`

#### Second code approach explanation (ENG)

```python
anagrams_dict = defaultdict(list)  # mapping charCount to list of Anagrams  
  
for word in strs:  
    count = [0] * 26  # 1
    for letter in word:  
        count[ord(letter) - ord('a')] += 1  # 2
  
    key = tuple(count)  # 3
    anagrams_dict[key].append(word)  # 4
  
return list(anagrams_dict.values())
```

Here our dict key is not just a str. Instead, we use hex code of each strs value `(a...00000..c..000..t...0)`

```python
"act"    →   "act"
"cat"    →   "act"
"pots"   →   "opst"
"tops"   →   "opst"
"stop"   →   "opst"
"hat"    →   "aht"

{
    (1, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0): ['act', 'cat'],
    (0, 0x11, 0, 1, 1, 1, 0, 0, 1, 1, 0, 0x4, 0): ['pots', 'tops', 'stop'],
    (1, 0, 0x4, 0, 1, 0, 0x9, , 0, 1, 0, 0x4, 0): ['hat']
}
```

NOTE: 0x11 or 0x9 means how many times 0 (zero) repeated. for example: 0x4 -> 0, 0, 0, 0

Why tuple ?
- Because every dict key must be immutable. `tuple is immutable`

1) We crete alphabet with 0 [0000 ..... n]
2) The hexadecimal index for letters starts at 95, 96, 97, 98, and so on — where A corresponds to 95, B to 96, C to 97, etc. By subtracting the hex index of A from the current letter’s hex index, we obtain an integer value starting from 0 up to 26. This approach helps us avoid starting from 95 and makes the process simpler and more convenient.
3) We convert `count` list into `key` touple
4) Add value to key for example: add `stop` value into `(0, 0x11, 0, 1, 1, 1, 0, 0, 1, 1, 0, 0x4, 0)`  -> `(0, 0x11, 0, 1, 1, 1, 0, 0, 1, 1, 0, 0x4, 0): stop`
