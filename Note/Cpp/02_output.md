# **C++ 筆記**
## 輸出 Output

# 基本架構  
```cpp
cout << "Hello World" << endl ;
```

這個語法是由三個以上的部分組合而成的  
分別是  

輸出  
```cpp
cout 
``` 

物件  
```cpp
"Hello World" 
```

換行  
```cpp
endl 
``` 

然後所東西之間都要用 ``` << ``` 區隔  
例如  

```cpp
cout << "Test" << "123" << endl ;
```
或  
```cpp
cout << "Test" << endl << "123" << endl ;
```

而接下來是程式碼本碼：  

```cpp
#include<bits/stdc++.h>
using namespace std;

int main(){
    
    cout << "Hello World" << endl ;
    
}
```

而這是運行結果  

```
Hello World
```

若把中間的``` "Hello World" ``` 換成別的，也會有相對應的結果  
例如  
```cpp
#include<bits/stdc++.h>
using namespace std;

int main(){
    
    cout << "Test" << "123" << endl ;
    
}
```

結果  

```
Test123
```

## 快樂的練習時間  

[TOJ 547](https://toj.tfcis.org/oj/pro/547/)  
