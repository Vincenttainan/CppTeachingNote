# **C++ 筆記**
## 輸入 Input

# 基本架構
```cpp
cin >> a;
```

cin >> 變數名稱 ;  

方向剛好跟輸出相反  

一個是in  大於大於；一個是out  小於小於  

```cpp
int a;
cin >> a;
```

有了變數這個容器後，我們就可以輸入了  

因為輸入的資料，需要有個容器（變數）儲存  

所以要在變數宣告，才能輸入資料  

```cpp
#include<bits/stdc++.h>
using namespace std;

int main(){
    
    int a;
    cin>>a;
    cout<<a<<endl;
    
}
```
上面就是關於輸入的一個簡單用法  

當然還可以做出更多  

例如：輸入長、寬計算長方形面積之類的  

```cpp
#include<bits/stdc++.h>
using namespace std;

int main(){
    
    int x,y;
    //宣告兩變數，分別代表長、寬
    cin>>x>>y;
    //輸入長方型長、寬
    cout<<x*y<<endl;
    //輸出長*寬（面積）
    
}
```

# 特殊輸入
```cpp
getline(cin,s);
```

當輸入的字串中可能含有空白時  
就需要使用`getline()`了  

例如，輸入  
```
Vincent tainan
```
用一般的  
```cpp
cin >> s;
cout << s << endl;
```
輸出會是`Vincent`而已  

然而若是用  
```cpp
getline(cin,s);
cout << s << endl;
```
輸出就會是`Vincent tainan`了  

## 快樂的練習時間

[TOJ 5](https://toj.tfcis.org/oj/pro/5/)  
[TOJ 92](https://toj.tfcis.org/oj/pro/92/)  
[TOJ 93](https://toj.tfcis.org/oj/pro/93/)  
[TOJ 98](https://toj.tfcis.org/oj/pro/98/)  
[TOJ 100](https://toj.tfcis.org/oj/pro/100/)  
[TOJ 101](https://toj.tfcis.org/oj/pro/101/)  
[TOJ 128](https://toj.tfcis.org/oj/pro/128/)  
[TOJ 339](https://toj.tfcis.org/oj/pro/339/)  
