# **Pyhton 筆記**  
## 輸出 Output  

# 基本架構  

```python
print( 物件A , 物件B , ... , sep = "X" , end = "Y" )
```

輸出 `物件A`, `物件B`, `...`  
並以 `X` 作為間隔，最後輸出 `Y`  
`sep`, `end` 可以不填  
預設 `sep` 為 `" "`  
預設 `end` 為 `"\n"`  

# 範例  
## 輸出單一物件  

### code  
```python
print( "Vincenttainan" )
```
### output  
```
Vincenttainan
```

## 輸出多種物件  

### code  
```python
a="Vincent"
b="tainan"
print( a , b )
```
### output  
```
Vincent tainan
```

## 更改間隔  

### code  
```python
a="Vincent"
b="tainan"
c="notorz"
print( a , b , c , sep=" ! " )
```
### output  
```
Vincent ! tainan ! notorz
```

## 更改換行  

### code  
```python
a="Vincent"
b="tainan"
print( a , b , end=" orz\n" )
```
### output  
```
Vincent tainan orz
```

## 更改間隔、換行  

### code  
```python
a="Vincent"
b="tainan"
c="notorz"
print( a , b , c , sep=" ! " , end=" orz\n" )
```
### output  
```
Vincent ! tainan ! notorz orz
```
