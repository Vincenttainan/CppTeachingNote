# **Pyhton 筆記**  
## 元組 tuple  

# 基本架構  

```python
tup1 = ("Vincent", "tainan", 888, 888, True)
tup2 = ("Vincenttainan", )
```

* 允許多個重複的元素  
* 允許 `tuple` 內的元素為不同型別  
* 使用 `()` 來表示 `tuple`  
* `tuple` 一但建立了，就無法修改內容  
* 就算 `tuple` 內只有一個元素，也要加上 `,`  

## index  

列表跟字串一樣，支援索引 `index` 來輔助存取元素  

Example:  

```python
tup1 = ("Vincent", "tainan", 888, 888, True)
```

|      List       | "Vincent" | "tainan" | 888 | 888 | True |
|:---------------:|:---------:|:--------:|:---:|:---:|:----:|
| Index from head |     0     |    1     |  2  |  3  |  4   |
| Index from tail |    -5     |    -4    | -3  | -2  |  -1  |

## 好處  

* 讀取速度較快  
* 佔用空間較少  
* 避免誤改資料  
