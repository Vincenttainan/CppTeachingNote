# **Pyhton 筆記**  
## 輸入 Input  

# 基本架構  

```python
input()
```
python 輸入必定為一字串，並且整行讀入  

# 範例  

## 輸入為一字串且在同一行內  

### input  
```
Vincent tainan
```
### code  
```python
a = input()
# a="Vincent tainan"
```

## 輸入為一數字  

### input  
```
123456789
```
### code  
```python
a = int( input() )
# a=123456789
```

## 輸入為兩個字串且在同一行  

### input  
```
Vincent tainan
```
### code  
```python
a, b = input().split()
# a="Vincent", b="tainan"
```

## 輸入為兩個字串且在同一行  

### input  
```
Vincent tainan
```
### code  
```python
a, b = input().split()
# a="Vincent", b="tainan"
```

## 輸入為兩個數字且在同一行  

### input  
```
12345 54321
```
### code  
```python
a, b = map( int, input().split() )
# a=12345, b=54321
```

## 輸入為不知道多少個字串且在同一行  

### input  
```
Vin cen tta ina n
```
### code  
```python
a = list( input().split() )
# a=["Vin", "cen", "tta", "ina", "n"]
```

## 輸入為不知道多少個數字且在同一行  

### input  
```
1 23 456 7890
```
### code  
```python
a = list( map(int, input().split() ) )
# a=[1, 23, 456, 7890]
```

## 輸入有一行，只有一個數字、一個字串  

### input  
```
48763 Vincenttainan
```
### code  
```python
a, b = map(str, input().split())
a = int(a)
# a=48763, b="Vincenttainan"
```
