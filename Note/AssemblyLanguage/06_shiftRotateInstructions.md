# **Assembly Language筆記**  
## 位移指令 shiftRotateInstructions  

---

## SHL / SAL   
### Shift Logical Left / Shift Arithmetic Left  

```asm
SHL destination, count
SAL destination, count
```

功能：將 `destination` 左移 `count` 位  
左邊空出來的位元補 `0`  

移出去的位元會進入 CF (Carry Flag)  
`SHL` 與 `SAL` 完全相同  

有號數 / 無號數 都一樣  

範例：  
```asm
MOV al, 00010110b   ; 22
SHL al, 1           ; 44 (乘 2)，CF = 原來的最高位
                    ; al = 00101100b
```

效果就是 乘以$2^n$（如果沒溢位）  

## SHR  
### Shift Logical Right  

```asm
SHR destination, count
```

功能：將 `destination` 邏輯右移 `count` 位  
右邊空出來的位元補 `0`  

移出去的位元進 CF  
常用於 無號數除法  

範例：  
```asm
MOV al, 00010110b   ; 22
SHR al, 1           ; 11 (除以 2)，CF = 原來的最低位
                    ; al = 00001011b
```

效果就是 無號數除以$2^n$  

## SAR  
### Shift Arithmetic Right  

```asm
SAR destination, count
```

功能：將 `destination` 算術右移 `count` 位  
右邊空出來的位元補「符號位」（最高位 = sign bit）  

移出去的位元進 CF  
常用於 有號數除法  

```asm
mov al, -22         ; 11101010b (補數)
sar al, 1           ; -11 (符號位保持 1)
                    ; al = 11110101
```

效果就是 有號數除以$2^n$，會向下取整  

## 常見差異比較  

| 指令  |   適用    | 左/右移 |    空位補什麼     |     用途      |
|:-----:|:---------:|:-------:|:-----------------:|:-------------:|
| `SHL` | 無號/有號 |  左移   |         0         |    乘$2^n$    |
| `SAL` | 無號/有號 |  左移   |         0         | 與 `SHL` 相同 |
| `SHR` |  無號數   |  右移   |         0         |    除$2^n$    |
| `SAR` |  有號數   |  右移   | 符號位 (sign bit) |    除$2^n$    |

## 快速乘法  

左移常用來 快速乘法（比 `MUL` 快很多）  

將要乘以的數看為2進制  
從最低位開始檢查：  

1. 若該位是 `1`，就把被乘數左移對應位數後加到結果  
2. 若該位是 `0`，就略過  

把所有結果加總  

---

## Rotate / 旋轉指令系列  

### 基本概念  

在 移位 `Shift` 中，超出的位元會被「丟掉」，空位補 0  
而在 旋轉 `Rotate` 中，超出的位元會「繞回」另一側  

### 四大旋轉指令  

| 指令 |            全名            |    中文名稱    |             功能              | 是否包含 CF |
|:----:|:--------------------------:|:--------------:|:-----------------------------:|:-----------:|
| ROL  |        Rotate Left         |     左旋轉     | 左移後，最高位 MSB 會補到 LSB |      X      |
| ROR  |        Rotate Right        |     右旋轉     | 右移後，最低位 LSB 會補到 MSB |      X      |
| RCL  | Rotate through Carry Left  | 經過 CF 左旋轉 | 左移，MSB 進 CF，CF 回補 LSB  |      V      |
| RCR  | Rotate through Carry Right | 經過 CF 右旋轉 | 右移，LSB 進 CF，CF 回補 MSB  |      V      |


## ROL / ROR  

### ROL（Rotate Left）  

```asm
mov al, 10110001b    ; AL = b10110001
rol al, 1            ; 向左旋轉 1 bit
; 結果：AL = b01100011
```

過程：  
```
10110001  (原)
└───────┐
 01100011 (最高位1繞到最右)
```

### ROR（Rotate Right）  

```asm
mov al, 10110001b    ; AL = b10110001
ror al, 1            ; 向右旋轉 1 bit
; 結果：AL = b11011000
```

過程：  
```
 10110001 (原)
┌───────┘
11011000  (最低位1繞到最左)
```

## RCL / RCR  

### RCL  
```asm
mov al, 10110001b  ; al = b10110001
stc                ; CF = 1
rcl al, 1
; 結果：AL = b01100011, CF = 1
```

過程：  
```
原： CF=1, AL=10110001

new CF = AL 最左邊 = 1
new AL = (AL - AL 最左邊) + CF = 01100011
```

### RCR  
```asm
mov al, 10110001b  ; al = b10110001
clc                ; CF = 0
rcr al, 1
; 結果：AL = b01011000, CF = 1
```

過程：  
```
原： CF=0, AL=10110001

new CF = AL 最右邊 = 1
new AL = CF + (AL - AL 最右邊) = 01011000
```
