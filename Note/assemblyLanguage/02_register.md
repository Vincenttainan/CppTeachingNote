# **Assembly Language筆記**  
## 暫存器 Register  

---

暫存器可以看成在 CPU 內的抽屜，數量很少但可以直接使用  
接下來是簡單的暫存器列表：  

| 名稱 |  大小   |                        說明                         |
|:----:|:-------:|:---------------------------------------------------:|
| EAX  | 32 bits |  累加器 (accumulator)，常用於運算結果、函式回傳值   |
| EBX  | 32 bits |  基底暫存器 (base register)，常用於記憶體位址運算   |
| ECX  | 32 bits |  計數器 (counter)，常用於迴圈 (loop) 與 shift 數量  |
| EDX  | 32 bits |      資料暫存器 (data register)，常用於乘除法       |
| ESI  | 32 bits |       來源索引 (source index)，字串/陣列操作        |
| EDI  | 32 bits |            目的索引 (destination index)             |
| EBP  | 32 bits | 基底指標 (base pointer)，常用於存取堆疊中的區域變數 |
| ESP  | 32 bits |       堆疊指標 (stack pointer)，指向堆疊頂端        |

> ▲ 暫存器簡表  

理論上，暫存器有常見用法  
但 EBX 可以放心跟 EAX一樣用於運算結果、函式回傳值  

---

但同時，因為不是所有運算都需要用滿 32 bits，例如只是計算 1+1 之類的  
所以其實暫存器可以拆成更小的部分  

| 名稱 |  大小   |                        說明                         |
|:----:|:-------:|:---------------------------------------------------:|
| EAX  | 32 bits |  累加器 (accumulator)，常用於運算結果、函式回傳值   |
|  AX  | 16 bits |                   EAX 的低 16 位                    |
|  AH  | 8 bits  |                    AX 的高 8 位                     |
|  AL  | 8 bits  |                    AX 的低 8 位                     |

```
名稱      所佔位置 （ 全部一共有32 bits ）

EAX    ||||||||||||||||||||||||||||||||
AX                     ||||||||||||||||
AH                     ||||||||
AL                             ||||||||
```
> ▲ 暫存器關係簡表（以 EAX 為例）  

| 32 bits | 16 bits | 高 8 bits | 低 8 bits |
|:-------:|:-------:|:---------:|:---------:|
|   EAX   |   AX    |    AH     |    AL     |
|   EBX   |   BX    |    BH     |    BL     |
|   ECX   |   CX    |    CH     |    CL     |
|   EDX   |   DX    |    DH     |    DL     |
|   ESI   |   SI    | 不可再拆  | 不可再拆  |
|   EDI   |   DI    | 不可再拆  | 不可再拆  |
|   EBP   |   BP    | 不可再拆  | 不可再拆  |
|   ESP   |   SP    | 不可再拆  | 不可再拆  |

### 與資料型態比較  

```asm
EAX ↔ DWORD (32-bit)

AX ↔ WORD (16-bit)

AL / AH ↔ BYTE (8-bit)
```
