Valid Anagram Question [link](https://leetcode.com/problems/valid-anagram/) from [[Leetcode]]

### ==**Code:**==
1) ==**O(N)**== (simple approach)
```python
if len(s) != len(t):  
    return False  
  
t_list = list(t)  
  
for char in s:  
    if char not in t_list:  
        return False  
    t_list.remove(char)  
  
return True
```

2) ==**O(N)**== (using HashMap)
```python
if len(s) != len(t):  
    return False  
  
l_map = {}  
for char in t:  
    l_map[char] = l_map.get(char, 0) + 1  
  
for char in s:  
    if char not in t or l_map[char] == 0:  
        return False  
    l_map[char] -= 1  
return True
```

3) ==**O(n log n)**==
```python
if sorted(list(s)) == sorted(list(t)):  
    return True  
return False  
```

3) ==**O(n log n)==
```python
return Counter(s) == Counter(t)
```

### ==Explanation on my words==

![[LeetCode P242.jpg]]

