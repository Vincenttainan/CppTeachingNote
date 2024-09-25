# **Pyhton 筆記**  
## 概論 Introduce  

# 基本架構  

```python
import math
# one line annotation
'''
more than one line
annotations
'''

if __name__ == '__main__':
    # main()
    
```

## 導入函式庫  

```python
import math
```

導入名叫 `math` 的函式庫  

---

## 主函式  

```python
if __name__ == '__main__':
    # main()
```

大部分的 code 都會在主函式中  
也就是在 `# main()` 的部分撰寫  

---

## 註解

```python
# one line annotation
'''
more than one line
annotations
'''
```

註解可以分成單行註解和多行註解  
如果註解只有單一行，那在最前面加上 `#` 就可以了  
而當註解超過一行時，那叫要在頭尾加上 `'''`  

---

然而，在簡單的程式專案時  
其實只要寫  

```python
import math
# one line annotation
'''
more than one line
annotations
'''

# main()
```

就可以了，不需要  

```python
if __name__ == '__main__':
    # main()
```
