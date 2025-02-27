# **Java 筆記**  
## 迴圈 loop  

Java 的迴圈主要有三種  

1. `for` 迴圈  
2. `while` 迴圈  
3. `do-while` 迴圈  

然後 Java 的 `for` 迴圈、 `while` 迴圈  
基本上跟 C++ 的一模一樣，所以就也不在這邊多做贅述  

所以這邊主要要講的是 `do-while` 迴圈  

## `do-while` 迴圈  

```java
do{
    /* your code here */
}while(/* condition */);
```

`do-while` 迴圈 跟 `while` 迴圈 其實很類似  
都是當條件為 `True` 便離開迴圈  
只是 `do-while` 迴圈 不論條件為何，都會先執行一次迴圈  
然後才去檢查條件  

## 範例  

### 程式碼  

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        int i=1;
        do{
            System.out.println(i);
            i++;
        }while(i<=0);
    }
}
```

### 輸出  
```
1
```

如果這邊是使用 `while` 迴圈  
在這樣的條件底下是不會輸出的  
但因為這邊使用了 `do-while` 迴圈  
所以不論如何都會先輸出一次  
