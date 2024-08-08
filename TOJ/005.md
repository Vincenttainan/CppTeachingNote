### [5 / Hello World!](https://toj.tfcis.org/oj/pro/5/)  
<details>

<summary>題目</summary>

### 題目敘述  
跟別人打招呼是一件有禮貌的事。來向大家打招呼吧！  
    
### 輸入說明  
輸入只有一行，為一個英文名字  
    
### 輸出說明  
向他打個招呼吧！名子加上 "Hello ,[name] !"(不含引號) 後輸出。  
    
### 輸入限制  
包含大小寫字母及空白，長度不超過20個字  
    
### 範例輸入
```
Peter
```

### 範例輸出
```
Hello ,Peter !
```

</details>
    
<details>

<summary>題解</summary>

第一眼，簡單的輸入輸出
```cpp
#include<bits/stdc++.h>
using namespace std;

int main() {
    string a;
    cin>>a;
    cout<<"Hello ,"<<a<<" !"<<endl;
}

```
然後就 WA 了，再看一眼題目  

### 輸入限制  
包含大小寫字母及 **空白** ，長度不超過20個字  

```cpp
#include<bits/stdc++.h>
using namespace std;

int main() {
    string a;
    getline(cin,a);
    cout<<"Hello ,"<<a<<" !"<<endl;
}
```
AC  

</details>
    
<details>

<summary>AC code</summary>

```cpp
#include<bits/stdc++.h>
using namespace std;

int main() {
    string a;
    getline(cin,a);
    cout<<"Hello ,"<<a<<" !"<<endl;
}
```

</details>
