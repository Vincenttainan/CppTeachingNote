# **Assembly Language筆記**  
## 副程式呼叫 callRetProcedures  

---

## CALL 指令  

```asm
call label
```

功能：  
先把 下一條指令位址 (EIP) 壓到堆疊 (push return address)  
跳到副程式的入口 (label)  

範例：  

```asm
main:
    mov eax, 5
    call myFunc     ; 呼叫副程式
    mov ebx, eax    ; 回來後繼續執行
    ret

myFunc:
    add eax, 3      ; eax = eax + 3
    ret             ; 返回 main
```

執行流程：  
* CALL -> 把 main 下一行的位址 push 到堆疊  
* 跳到 `myFunc`  
* 執行 `add eax, 3`  
* RET → 從堆疊 pop 出 return address -> 回到 main  

## RET 指令  

```asm
RET
```

功能：  
從堆疊 彈出 return address，並跳回該位址繼續執行  

進階：  

```asm
RET n
```

除了回傳，還會把堆疊指標 (ESP) 再加上 n -> 通常用於「清理參數」  

## 帶參數的副程式  

### 呼叫者 (Caller) 負責推參數  

```asm
main:
    push 3             ; 傳遞參數 y
                       ; stack = 3 <- push
    push 5             ; 傳遞參數 x
                       ; stack = 3, 5 <- push

    ; stack now = [esp][esp+4][esp+8]
    ;             [ret][  5  ][  3  ]

    call addFunc       ; 呼叫副程式

    add esp, 8         ; esp = esp+8 
    
    ; stack now = [esp][esp+4][esp+8]
    ;               |            ^
    ;               └────────────┘

    mov ebx, eax       ; ebx = eax = 8
    ret                ; return

addFunc:
    ; stack now = [esp][esp+4][esp+8]
    ;             [ret][  5  ][  3  ]
    
    mov eax, [esp+4]   ; eax = 5
    mov ecx, [esp+8]   ; ecx = 3
    add eax, ecx       ; eax = 5 + 3 = 8
    ret                ; return
```

流程：  

1. Caller push 參數（順序通常右到左）  
2. CALL push return address，再跳到副程式  
3. 副程式從 [ESP+4], [ESP+8] 取到參數  
4. RET 回去，Caller 自己清堆疊  

### 範例： f(x,y) = max(x,y)  

```asm
main:
    mov eax, 10     ; eax = 10
    mov ebx, 20     ; ebx = 20
    push ebx        ; 傳遞參數 y
                    ; stack = 20 <- push
    push eax        ; 傳遞參數 x
                    ; stack = 20, 10 <- push
                    
    ; stack now = [esp][esp+4][esp+8]
    ;             [ret][ 20  ][ 10  ]
    
    call maxFunc    ; 呼叫副程式
    
    add esp, 8
    
    ; stack now = [esp][esp+4][esp+8]
    ;               |            ^
    ;               └────────────┘
    
    ; eax = max(x, y)
    ret              ; return

maxFunc:
    ; stack now = [esp][esp+4][esp+8]
    ;             [ret][ 20  ][ 10  ]

    mov eax, [esp+4] ; eax = 20
    mov ecx, [esp+8] ; ecx = 10
    cmp eax, ecx     ; eax - ecx
    jge end_max      ; if eax >= ecx --> go to end_max
    mov eax, ecx     ; else --> eax = ecx

end_max:
    ret              ; return
```
