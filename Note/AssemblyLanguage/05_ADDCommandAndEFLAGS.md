# **Assembly Language筆記**  
## ADD系列指令與EFLAGS ADDCommandAndEFLAGS  

---

## ADD  

```asm
ADD destination, value
```

功能：`destination = destination + value`  
`value` 可以是 立即值、暫存器、記憶體  
結果會影響旗標暫存器 (EFLAGS)  

範例：  
```asm
MOV eax, 5
ADD eax, 3    ; eax = 8
```

## SUB  

```asm
SUB destination, value
```

功能：`destination = destination - value`  
`value` 可以是 立即值、暫存器、記憶體  
結果會影響旗標暫存器 (EFLAGS)  

範例：  
```asm
MOV eax, 5
SUB eax, 3    ; eax = 2
```

## INC / DEC  

```asm
INC destination
DEC destination
```

INC：加 1  
DEC：減 1  

幾乎等價於 `ADD reg, 1` / `SUB reg, 1`，但程式碼比較短  

特殊點：不會影響 `Carry Flag (CF)`  

範例：  
```asm
mov eax, 0FFFFFFFFh
inc eax      ; eax = 0, ZF=1, 但 CF 不會設成1
```

## EFLAGS  

執行 `ADD` / `SUB` / `INC` / `DEC` 會影響以下旗標：  

| 旗標 |     名稱      |         何時設為 1          |      說明      |
|:----:|:-------------:|:---------------------------:|:--------------:|
|  CF  |  Carry Flag   | 無號加法進位 / 無號減法借位 | 無號數溢出偵測 |
|  OF  | Overflow Flag |       有號數超過範圍        | 有號數溢出偵測 |
|  ZF  |   Zero Flag   |          結果 = 0           |                |
|  SF  |   Sign Flag   |       結果最高位 = 1        |    負數判斷    |

範例：  

```asm
; 無號數情境 (CF 檢查)
mov al, 255    ; 0xFF
add al, 1      ; al=0, CF=1, OF=0

; 有號數情境 (OF 檢查)
mov al, 127    ; 0x7F (有號數最大正整數)
add al, 1      ; al=0x80 (-128)，OF=1, CF=0
```

* 無號數看 CF  
* 有號數看 OF  
