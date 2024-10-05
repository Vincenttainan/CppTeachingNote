# **Pyhton 筆記**  
## 列表 List  

# 基本架構  

```python
lst = ["Vincent", "tainan", 888, 888, True]
```

* 允許多個重複的元素  
* 允許 `list` 內的元素為不同型別  
* 使用 `[]` 來表示 `list`  

## index  

列表跟字串一樣，支援索引 `index` 來輔助存取元素  

Example:  

```python
lst = ["Vincent", "tainan", 888, 888, True]
```

|      List       | "Vincent" | "tainan" | 888 | 888 | True |
|:---------------:|:---------:|:--------:|:---:|:---:|:----:|
| Index from head |     0     |    1     |  2  |  3  |  4   |
| Index from tail |    -5     |    -4    | -3  | -2  |  -1  |

## function  

* len( lst )  
回傳 `lst` 的長度  
* list( s )  
將 `s` 轉為列表  
* lst.clear()  
清空 `lst`  
* lst.pop( a )  
移出 `lst` 中，位置在 `a` 的元素  
* lst.append( a )  
將 `a` 植入 `lst` 的尾端  
* lst.extend( lst2 )  
將 `lst2` 的值 植入 `lst` 的尾端  
* lst.remove( a )  
將 `lst` 內的 `a` 移除  
* lst.reverse()  
將 `lst` 頭尾翻轉  
* lst.count( a , start , end )  
從 `start` 到 `end` 中，共有多少個 `a`  
