# **Java 筆記**  
## 輸出 Output  

在 Java 中，輸出主要有兩種方式  

1. `System.out.println()`  
用這種方式輸出會自動換行  

2. `System.out.print()`  
用這種方式輸出不會換行  
如果要換行需要在最後加上`\n`  

## 範例  

### 程式碼  
```java
public class Main {
    public static void main(String[] args) {
        System.out.print("This is print.");
        System.out.print("This is print with newline\n");
        System.out.println("This is println");
    }
}
```

### 輸出結果  
```
This is print.This is print with newline
This is println
```
