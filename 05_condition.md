# **程式 筆記**  
## 條件 Condition  

# 基本架構  
```cpp
if(condition_1){
    //do when condition_1 is true
}
else if(condition_2){
    //do when condition_1 is not true and condition_2 is true
}
else{
    //do when condition_1 and condition_2 is both not ture
}
```

條件：所有的條件，最後都要能變成 true / false 其中之一  

舉個例子：  
```cpp
if(口渴了){
    喝水
}
```

例如我們想知道一個輸入有沒有大於 10  

```cpp
#include<bits/stdc++.h>
using namespace std;

int main(){
    
    int a;
    cin>>a;
    if(a>10){
        cout << "大於10" <<endl;
    }
    
}
```
