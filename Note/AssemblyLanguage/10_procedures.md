# **Assembly Language筆記**  
## 副程式 procedure  

---

## PROC（Procedure）  

```asm
MyFunc PROC
    ; 副程式內容
    ret
MyFunc ENDP
```

* `PROC` = 宣告副程式的開始  
* `ENDP` = 宣告副程式的結束  
* 名字（例：`MyFunc`）就是標籤，可以被 CALL 呼叫  

這樣寫的效果，和用 `label:` 開頭差不多，但更清楚表示「這是副程式」  

## 範例一：無參數副程式  

```asm
main PROC
    mov eax, 5
    call add3
    mov ebx, eax
    ret
main ENDP

add3 PROC
    add eax, 3
    ret
add3 ENDP
```

執行流程：  

1. `call add3` -> 把 `return address` push 到堆疊  
2. 跳去 `add3`，執行 `add eax, 3`  
3. `ret` -> 回到 `main`  

## 範例二：有參數副程式  

在 MASM 裡，`PROC` 可以直接宣告參數和區域變數  
組譯器會自動幫你對應 stack  

### 呼叫方式  

```asm
push y
push x
call addFunc
```

### 定義方式  

```asm
addFunc PROC x:DWORD, y:DWORD
    mov eax, x      ; eax = x
    add eax, y      ; eax = x + y
    ret
addFunc ENDP
```

這樣就不用自己 `[esp+4]`、`[esp+8]`  
MASM 會自動幫你對應名稱  

## 範例三：區域變數  

```asm
sum PROC x:DWORD, y:DWORD
    LOCAL result:DWORD

    mov eax, x
    add eax, y
    mov result, eax   ; 存到區域變數
    mov eax, result   ; 回傳值放 eax
    ret
sum ENDP

```
