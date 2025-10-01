# **Assembly Language筆記**  
## PUSH/POP與堆疊 PUSH/POPandStack

---

## 什麼是 Stack  

堆疊是一塊 後進先出 (LIFO) 的記憶體區域  
ESP(Stack Pointer) 指向「堆疊頂端」  

在 x86 中，Stack 向下成長（往低位址推）  

```
高位址
       |    (空)     
       |------------
       |    舊資料
       |------------
       | <- ESP
低位址
```

## PUSH  

```asm
PUSH register
PUSH memory
PUSH immediate
```

功能：將一個值壓入堆疊  
值可以是 暫存器、記憶體、立即值  

步驟：  

1. ESP = ESP - 4 (32-bit 模式，因為壓入 dword)  
2. 把值存到 [ESP]  

範例：  

```asm
MOV  eax, 1234h
PUSH eax      ; [ESP] = 1234h
```

## POP  

```asm
POP reg
POP mem
```

功能：從堆疊頂取出一個值，放到暫存器 / 記憶體  

步驟：  

1. 取 [ESP]  
2. ESP = ESP + 4  

範例：  

```asm
pop ebx       ; ebx = [ESP], ESP+4
```

## PUSH POP 搭配  

```asm
push val1       ; stack = val1 <-in
push val2       ; stack = val1, val2 <-in

pop eax         ; eax = val2
                ; stack = val1 -> out
pop ebx         ; ebx = val1
                ; stack = (empty) -> out
```

## 保存暫存器狀態  

```asm
push eax
push ebx

; ... 一番激烈的運算 ...

pop ebx
pop eax
```

這樣可以確保做運算前後，暫存器值不會被破壞  

## 特殊 PUSH/POP 指令  

`PUSHF` ： 把 EFLAGS 壓入堆疊  
`POPF` ： 從堆疊還原 EFLAGS  

`PUSHA` ： 把 AX, CX, DX, BX, SP, BP, SI, DI 全部壓入  
`POPA` ： 全部還原  

## 注意事項  

1. PUSH/POP 在 32-bit 下是 一次 4 bytes (dword)  
   在 16-bit 下則是 一次 2 bytes (word)  

2. 如果 PUSH 和 POP 不平衡，會導致 RET 跳到錯誤位置 -> crash  
