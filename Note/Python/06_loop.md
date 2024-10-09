# **Pyhton 筆記**  
## 迴圈 Loop  

# for loop  
## 基本架構  

```python
for i in range( A , B , C ):
    # code
```

從 `A` 開始每次加 `C` 直到超過 `B`  

### code  
```python
for i in range(0,10,1):
    print("*",end="")
```

### output  
```
**********
```

---

# while loop  
## 基本架構  

```python
while condition:
	#code
```

每次判斷 `condition` 是否為真  
若為真，便執行  
否則，離開迴圈  

### code  
```python
n=0
while n<5:
    print(n)
    n+=1
```

### output  
```
0
1
2
3
4
```

---

# 迴圈內可用的語法  

## break  
直接離開迴圈，終止迴圈  

## continue  
跳過這次的迴圈，直接執行下一圈  

### code  
```python
for i in range(0,10,1):
    if i%2==0:
        continue
    if i==7:
        break
    print(i)
```

### output  
```
1
3
5
```

---

# 補充  

## 輸入直到 eof 為止  

```python
while True:
    try: 
        # code
    except EOFError:
        break
```
