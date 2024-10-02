# **Pyhton 筆記**  
## 條件 Condition  

# 基本架構  

```python
if condition1:
    #code1
elif condition2:
    #code2
else:
    #code3
```
判斷條件 `condition1` 是否正確  
若正確，便執行 `code1`  
否則判斷條件 `condition2` 是否正確  
若正確，便執行 `code2`  
否則便執行 `code3`  

```mermaid
flowchart LR
程式開始 --> C1{condition1} --> |True|code1 --> 程式結束
C1 --> |False|C2{condition2} --> |True|code2 --> 程式結束
C2 --> |False|code3 --> 程式結束
```

## 其他範例  

```python
if condition1:
    #code1
elif condition2:
    #code2
if condition3:
    #code3
else:
    #code4
```

```mermaid
flowchart LR
程式開始 --> C1{condition1} --> |True|code1
C1 --> |False|C2{condition2} --> |True|code2
C2 --> |False|C3
code1 --> C3{condition3} --> |True|code3
code2 --> C3 --> |False|code4
code3 --> 程式結束
code4 --> 程式結束
```
