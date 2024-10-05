# **Pyhton 筆記**  
## 字串 String  

# 基本架構  

```python
s1 = 'Vincenttainan'
# s1 = Vincenttainan
s2 = "Vincent tainan"
# s2 = Vincent tainan
s3 = '''
This is 
Vincenttainan 
form 
Tainan
'''
# s3 = This is \nVincenttainan \nform \nTainan
```

* 短字串可以用一對單引號或是一對雙引號所組成  
* 長字串可以用一對三個單引號所組成  

## index  

字串支援索引 `index` 來輔助存取字元  

Example:  
`s = "Vincenttainan"`  

| String | V | i | n | c | e | n | t | t | a | i | n | a | n |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Index from head | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 |
| Index from tail | -13 | -12 | -11 | -10 | -9 | -8 | -7 | -6 | -5 | -4 | -3 | -2 | -1 |

## slicing  

字串支援切割 `slicing` 來輔助存取字元  

```python
s[start : end : interval]
```

Example:  
`s = "Vincenttainan"`  

`s[2:]` = `ncenttainan`  
`s[:-2]` = `Vincenttain`  
`s[2:-2]` = `ncenttain`  
`s[2:-2:2]` = `netan`  
`s[::-1]` = `naniattnecniV`  

## connecting  

字串連結、字串重複  

```python
s1 = "Vincent"
s2 = "tainan"
s3 = s1+s2
# s3 = "Vincenttainan"
s4 = s1+s2*2
# s4 = "Vincenttainantainan"
```

## function  

* len(s)  
回傳字串 `s` 的長度  
* s.upper()  
把字串 `s` 全改成大寫  
* s.lower()  
把字串 `s` 全改成小寫  
* s.isupper()  
回傳字串 `s` 是否全為大寫  
* s.islower()  
回傳字串 `s` 是否全為小寫  
* s.find( s2 )  
回傳字串 `s` 中 `s2` 的位置  
* s.replace( s2 , s3 , n )  
把字串 `s` 中 `s2` 改為 `s3` ，最多做 `n` 次  
* max(s)  
回傳 `s` 內 acsii 最大的字元  
* min(s)  
回傳 `s` 內 acsii 最小的字元  
* x in s  
如果 `x` 在 `s` 內，回傳 true，否則回傳 false  
