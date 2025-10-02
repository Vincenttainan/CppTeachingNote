# **Assembly Language筆記**  
## 比較跳躍與迴圈 conditionalControlFlowAndLoop  

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

## LOOP 指令  

```asm
label:
    ; command
    LOOP label
```

功能：自動遞減 CX 暫存器，如果 CX != 0，則跳到指定標籤  

動作：  
1. CX = CX – 1  
2. 如果 CX != 0，跳到 label；否則繼續往下執行  

常用於迴圈控制，必須先設定 CX = 次數  

範例：重複加總 10 次  

```asm
MOV CX, 10        ; 設定迴圈次數
MOV AX, 0
MOV BX, 1

LOOP_START:
    ADD AX, BX    ; AX = AX + BX
    INC BX        ; BX++
    LOOP LOOP_START
```

| counter |  i  | ii  | iii | iv  |  v  | vi  | vii | iix | ix  |  x  | xi  |
|:-------:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| **AX**  |  0  |  1  |  3  |  6  | 10  | 15  | 21  | 28  | 36  | 45  | 55  |
| **BX**  |  1  |  2  |  3  |  4  |  5  |  6  |  7  |  8  |  9  | 10  | 11  |
| **CX**  | 10  |  9  |  8  |  7  |  6  |  5  |  4  |  3  |  2  |  1  |  0  |
