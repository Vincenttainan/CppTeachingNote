# **Assembly Language筆記**  
## 乘法除法指令 mulDivInstruction  

---

## 整體概念  

| 指令 | 類型 | 有號 / 無號 |                      功能                      |
|:----:|:----:|:-----------:|:----------------------------------------------:|
| MUL  | 乘法 |    無號     | AL×r / AX×r / EAX×r → 結果放在兩倍大小的暫存器 |
| IMUL | 乘法 |    有號     |              同上，但支援有號整數              |
| DIV  | 除法 |    無號     |            DX:AX ÷ r / EDX:EAX ÷ r             |
| IDIV | 除法 |    有號     |                同上，但支援負數                |

## 乘法系列  

### MUL ( 無號乘法 )  

語法：  
```asm
mul r/m
```

功能：  

EAX（或 AX / AL）與指定運算元相乘，結果存入更大的暫存器組合中  

|  運算元大小  |  隱含暫存器  |  結果暫存器  |
|:----------:|:-----------:|:----------:|
|   8-bit    |  AL × r/m8  |     AX     |
|   16-bit   | AX × r/m16  |   DX:AX    |
|   32-bit   | EAX × r/m32 |  EDX:EAX   |

#### 範例 8-bit  

```asm
mov al, 5
mov bl, 6
mul bl          ; AL × BL = 30
; AX = 0030h
; AH = 00h, AL = 30h
```

#### 範例 16-bit  

```asm
mov ax, 2000h
mov bx, 10h
mul bx
; DX:AX = 2000h × 10h = 20000h
; DX = 0002h, AX = 0000h
```

### 注意  

* `MUL` 結果比原始運算元寬一倍  
* 若結果超過目的暫存器可容納的大小，會設 `CF=1`、`OF=1`  

### IMUL ( 有號乘法 )  

語法有三種版本  

1. 單一運算元（最簡）  
```asm
IMUL r/m
```
> 和 MUL 相同，但有號  
> AL, AX, EAX * r/m

2. 兩運算元版本  
```asm
IMUL reg, r/m
```
> reg = reg * r/m  

3. 三運算元版本（最靈活）  
```asm
IMUL reg, r/m, imm
```
> reg = r/m × imm  

#### 範例  

```asm
mov ax, 7
mov bx, -3
imul bx
; DX:AX = ax × bx
; DX:AX = 7 × (-3) = -21
; DX:AX = FFFF:FFEBh
```

```asm
mov eax, 10
imul eax, 3
; eax = eax × 3
; eax = 10 × 3
; eax = 30

imul eax, eax, -2
; eax = eax × -2
; eax = 30 × -2
; eax = -60
```

## 除法系列  

### DIV ( 無號除法 )  

```asm
DIV r/m
```

功能：  

用「被除數」÷「運算元」，自動分配到固定暫存器中  

| 除數大小  |  被除數暫存器  |        結果        |
|:--------:|:------------:|:-----------------:|
|  8-bit   | AX ( AH:AL ) |  餘 → AH，商 → AL  |
|  16-bit  |    DX:AX     |  餘 → DX，商 → AX  |
|  32-bit  |   EDX:EAX    | 餘 → EDX，商 → EAX |

#### 範例 8-bit  

```asm
mov ax, 25      ; AH:AL = 0:25
mov bl, 4
div bl
; AH = AL % BL = 25 % 4 = 1 → 餘
; AL = AL / BL = 25 / 4 = 6 → 商
; AX = 0106
```

#### 範例 32-bit  

```asm
mov edx, 0
mov eax, 20
mov ebx, 3
div ebx
; EDX = EAX % EBX = 20 % 3 = 2 → 餘
; EAX = EAX / EBX = 20 / 3 = 6 → 商
```

### 注意：  

* 在除法前要確保高位暫存器 (AH 或 DX 或 EDX) 為 0，否則結果會錯  
* 若除數 = 0 或商太大放不下 → 觸發「除法錯誤（#DE）」例外  

### IDIV ( 有號除法 )  

與 DIV 類似，但支援負數  
被除數需要以「符號擴展」準備好：  

|  除數大小  |  被除數暫存器  |        結果         |
|:--------:|:------------:|:------------------:|
|  8-bit   | AX ( AH:AL ) |  餘 → AH，商 → AL   |
|  16-bit  |    DX:AX     |  餘 → DX，商 → AX   |
|  32-bit  |   EDX:EAX    | 餘 → EDX，商 → EAX  |

#### 範例  

```asm
mov eax, -20
cdq            ; 符號擴展 EAX → EDX:EAX
mov ebx, 3
idiv ebx
; EDX = EAX % EBX = -20 % 3 = -2 → 餘
; EAX = EAX / EBX = -20 / 3 = -6 → 商
```

### 輔助指令  

| 指令  |              全名               |          功能            |
|:-----:|:------------------------------:|:-----------------------:|
| `CBW` |      Convert Byte to Word      |    AL → AX（符號擴展）    |
| `CWD` |   Convert Word to Doubleword   |  AX → DX:AX（符號擴展）   |
| `CDQ` | Convert Doubleword to Quadword | EAX → EDX:EAX（符號擴展） |

通常在使用 `IDIV` 前使用，確保高位元正確擴展符號  

### 實戰示例：計算 `(-12) ÷ 5`  

```asm
mov eax, -12    ; EAX = -12 = 1111111111110100b
                ;           = F   F   F   4   h    ( 其實不用轉乘 hex )
cdq             ; EDX:EAX = FFFF:FFF4h             ( 其實不用轉乘 hex )
mov ebx, 5      ; EBX = 5
idiv ebx
; EDX = EAX % EBX = -12 % 5 = -2 → 餘
; EAX = EAX / EBX = -12 / 5 = -2 → 商
```

### 小結表  

| 指令 | 有號 |    被除數 / 被乘數     |       結果暫存器       |  備註  |
|:----:|:----:|:----------------------:|:----------------------:|:------:|
| MUL  |  X   |    `AL`/`AX`/`EAX`     | `AX`/`DX:AX`/`EDX:EAX` | 無號乘 |
| IMUL |  V   |       同上或自訂       |          同上          | 有號乘 |
| DIV  |  X   | `AX`/`DX:AX`/`EDX:EAX` |         餘:商          | 無號除 |
| IDIV |  V   |          同上          |         餘:商          | 有號除 |

商:餘 = `AH:AL` / `DX:AX` / `EDX:EAX`
