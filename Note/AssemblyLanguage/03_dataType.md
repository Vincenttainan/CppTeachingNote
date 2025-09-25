# **Assembly Language筆記**  
## 資料型態 DataType  

---

### 整數部分  

| 關鍵字 |     大小      | 範圍 (Unsigned) |     範圍 (Signed, 二補數)     |              說明              |
|:------:|:-------------:|:---------------:|:-----------------------------:|:------------------------------:|
|  BYTE  |  8 bits (1B)  |      0~255      |               –               |          無號 8 位元           |
| SBYTE  |  8 bits (1B)  |        –        |           -128~+127           |          有號 8 位元           |
|  WORD  | 16 bits (2B)  |    0~65,535     |               –               |          無號 16 位元          |
| SWORD  | 16 bits (2B)  |        –        |        -32,768~+32,767        |          有號 16 位元          |
| DWORD  | 32 bits (4B)  | 0~4,294,967,295 |               –               |          無號 32 位元          |
| SDWORD | 32 bits (4B)  |        –        | -2,147,483,648~+2,147,483,647 |          有號 32 位元          |
| QWORD  | 64 bits (8B)  |    0~2^64-1     |               –               |          無號 64 位元          |
| SQWORD | 64 bits (8B)  |        –        |       -(2^63)~+(2^63-1)       |          有號 64 位元          |
| TBYTE  | 80 bits (10B) |        –        |               –               | Extended integer / FPU special |

### 浮點數部分  

| 關鍵字 |     大小      |               說明                |
|:------:|:-------------:|:---------------------------------:|
| REAL4  | 32 bits (4B)  |       單精度浮點數 (float)        |
| REAL8  | 64 bits (8B)  |       雙精度浮點數 (double)       |
| REAL10 | 80 bits (10B) | Extended precision (x87 FPU 專用) |

### 字元與字串  

`byte` 常常來用存儲字元（ 以 ASCII ）  
而字串則是使用 `byte` 陣列  

```asm
msg BYTE "HELLO", 0     ; 以 0 作為字串結尾
```

### 與暫存器比較  

```asm
EAX ↔ DWORD (32-bit)

AX ↔ WORD (16-bit)

AL / AH ↔ BYTE (8-bit)
```
