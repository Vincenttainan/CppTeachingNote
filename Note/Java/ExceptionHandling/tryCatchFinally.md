# **Java 筆記**  
## 例外處理 tryCatchFinally  

### 什麼是例外？  

在 Java 中， **例外** 是在程式執行時發生的錯誤，例如：

* 除以 0（`ArithmeticException`）
* 陣列超出範圍（`ArrayIndexOutOfBoundsException`）
* 讀取不存在的檔案（`FileNotFoundException`）

這些錯誤會導致程式 **異常終止**  
但可以透過 **例外處理機制** 來應對  
確保程式不會直接崩潰  

### `try-catch-finally`  

#### `try-catch` 的基本用法  

可以使用 `try` 和 `catch` 來捕捉並處理例外  

```java
public class Main {
    public static void main(String[] args) {
        try{
            int ans=10/0;
            System.out.println(ans);
        }
        catch(ArithmeticException e){
            System.out.println("Can't divide 0");
        }
        System.out.println("Still running");
    }
}

```

```
Can't divide 0
Still running
```

因為 `try` 這塊區塊內會發生 `ArithmeticException`  
而 `catch` 這塊區塊則會捕捉他，用以防止程式崩潰  

#### `finally` 區塊  

有發生錯誤：  
```java
public class Main {
    public static void main(String[] args) {
        try{
            int ans=10/0;
            System.out.println(ans);
        }
        catch(ArithmeticException e){
            System.out.println("Can't divide 0");
        }
        finally{
            System.out.println("This block runs always");
        }
        System.out.println("Still running");
    }
}
```

```
Can't divide 0
This block runs always
Still running
```

無發生錯誤：  
```java
public class Main {
    public static void main(String[] args) {
        try{
            int ans=10/2;
            System.out.println(ans);
        }
        catch(ArithmeticException e){
            System.out.println("Can't divide 0");
        }
        finally{
            System.out.println("This block runs always");
        }
        System.out.println("Still running");
    }
}
```

```
5
This block runs always
Still running
```

即使沒有發生例外，`finally` 仍然會執行  
