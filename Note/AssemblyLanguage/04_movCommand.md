# **Assembly Language筆記**  
## MOV系列指令 MOVCommand  

---

## MOV  
最基本的搬移  

#### 語法：  
```asm
MOV destination, value
```

#### 功能：  
把 `value` 的值複製到 `destination`  

#### 注意：位元大小必須一致  


| 指令 |    用法    |          範例          |              說明               |
|:----:|:----------:|:----------------------:|:-------------------------------:|
| mov  | 同大小搬移 |      `mov eax, ebx`      |  把 EBX 的 32-bit 值複製到 EAX  |
|      |            | `mov al, BYTE PTR [var]` | 把記憶體變數的 8-bit 值放到 AL  |
|      |            | `mov ax, WORD PTR [var]` | 把記憶體變數的 16-bit 值放到 AX |

### MOV的朋友：強制型別轉換  

當編譯器遇到模糊的情況時，例如：  
編譯器不知道到底要存 8-bit 還是 16-bit？  

```asm
mov [var], 1
```

就必須靠 `PTR` 來告訴編譯器這次操作的大小：  

```asm
mov BYTE PTR [var], 1   ; 強制當成 8-bit
mov WORD PTR [var], 1   ; 強制當成 16-bit
mov DWORD PTR [var], 1  ; 強制當成 32-bit
```

## MOVZX (Move with Zero-Extend)  
將東西以 0 延展並搬移  

#### 語法：  
```asm
MOVZX destination, value
```

#### 功能：  
把小型來源 (8/16 位元) 搬移到大暫存器，並在左邊補 0  

| 指令  |    用法     |            範例             |                       說明                       |
|:-----:|:-----------:|:---------------------------:|:------------------------------------------------:|
| movzx | 擴展 (補 0) |       `movzx eax, al`       | 把 AL (8-bit) 搬到 EAX (32-bit)，高 24 bits 補 0 |

## MOVSX (Move with Sign-Extend)  
將東西以符號延展並搬移  

#### 語法：  
```asm
MOVSX destination, value
```

#### 功能：  
把小型來源 (8/16 位元) 搬移到大暫存器，並進行符號延伸  
若最高位元是 1，則補 1；否則補 0  

| 指令  |      用法       |      範例       |                     說明                      |
|:-----:|:---------------:|:---------------:|:---------------------------------------------:|
| movsx | 擴展 (符號延伸) | `movsx eax, al` | 若 AL = `0FFh` (=-1)，搬到 EAX 變 `FFFFFFFFh` |

## 範例：  

```asm
.data
    val8   SBYTE  -5       ; 有號 8-bit (-5 = FBh)
    val16  SWORD  -1234    ; 有號 16-bit
    val32  SDWORD 12345678h

.code
main PROC
    ; 基本搬移
    mov     al, BYTE PTR val8       ; AL = FBh
    mov     ax, WORD PTR val16      ; AX = FB2Eh

    ; movzx → 補 0
    movzx   eax, BYTE PTR val8      ; EAX = 000000FBh
    movzx   eax, WORD PTR val16     ; EAX = 0000FB2Eh

    ; movsx → 符號延伸
    movsx   eax, BYTE PTR val8      ; EAX = FFFFFFFBh (=-5)
    movsx   eax, WORD PTR val16     ; EAX = FFFFFB2Eh (=-1234)

    exit
main ENDP
END main

```
