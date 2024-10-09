# **Pyhton 筆記**  
## 函式 Function  

# 基本架構  

### code  

```python
def function_name(input1, input2, input3 ......):
    #your code here
    return result
```

例如這是一個計算圓面積的函式  

### code  

```python
def circle_calculator(r):
    return r*r*3
print(circle_calculator(10))
```

### output  

```
300
```

又例如這是一個計算圓面積或圓周長的函式  

### code  

```python
def circle_calculator(r, is_area=True):
    if is_area:
        return r*r*3
    else:
        return 2*r*3
print(circle_calculator(10,1))
print(circle_calculator(10,0))
print(circle_calculator(10))
```

### output  

```
300
60
300
```

這裡因為 `is_area` 參數是有預設值是 `True`  
所以如果沒有得到輸入的話就會看作是 `True`  

又又例如這是一個計算圓面積或圓周長的函式  

### code  

```python
def circle_calculator(r, is_area=True):
    def t(x,y):
        return x*y
    
    if is_area:
        return t(r,r)*3
    else:
        return t(2,r)*3
print(circle_calculator(10,1))
print(circle_calculator(10,0))
print(circle_calculator(10))
```

### output  

```
300
60
300
```

從這份程式可以發現  
在任何需要的地方  
都可以宣告一個函式出來  
