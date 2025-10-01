# **Assembly Language筆記**  
## 比較與跳躍 conditionalControlFlow  

---

## CMP 指令  

```asm
CMP destination, source
```

功能：做 destination - source 的比較  
但不存結果，只影響 EFLAGS。  

* ZF (Zero Flag) → 是否相等  
* SF (Sign Flag) → 正負號  
* CF (Carry Flag) → 無號數大小  
* OF (Overflow Flag) → 有號數溢位  

範例：  

```asm
mov eax, 5
cmp eax, 5    ; ZF=1 (相等)
cmp eax, 3    ; ZF=0, CF=0, SF=0 (大於)
cmp eax, 7    ; ZF=0, CF=1 (小於)
```

## 無條件跳躍  

```asm
JMP label
```

直接跳到 `label`，不管任何條件  

## 條件跳躍 (依據 EFLAGS)  

條件跳躍的英文縮寫很多，但大致分兩類：  

### 1. 無號數比較  

|   指令    |     條件     |           說明            |
|:---------:|:------------:|:-------------------------:|
|  JE / JZ  |     ZF=1     |           相等            |
| JNE / JNZ |     ZF=0     |          不相等           |
|    JA     | CF=0 且 ZF=0 |       大於 (Above)        |
|    JAE    |     CF=0     | 大於等於 (Above or Equal) |
|    JB     |     CF=1     |       小於 (Below)        |
|    JBE    | CF=1 或 ZF=1 |         小於等於          |

### 2. 有號數比較  

|   指令    |     條件      |      說明      |
|:---------:|:-------------:|:--------------:|
|  JE / JZ  |     ZF=1      |      相等      |
| JNE / JNZ |     ZF=0      |     不相等     |
|    JG     | ZF=0 且 SF=OF | 大於 (Greater) |
|    JGE    |     SF=OF     |    大於等於    |
|    JL     |     SF≠OF     |  小於 (Less)   |
|    JLE    | ZF=1 或 SF≠OF |    小於等於    |

範例：if-else  

```asm
mov eax, 5
cmp eax, 3
jg  greater       ; 如果 eax > 3，跳到 greater

mov ebx, 0        ; else 部分
jmp end_if

greater:
    mov ebx, 1

end_if:
```

範例：while 迴圈  

```asm
mov ecx, 5       ; 計數器 = 5

while_start:
    cmp ecx, 0
    jle while_end ; 如果 ecx <= 0 就跳出
    dec ecx
    jmp while_start

while_end:
```

