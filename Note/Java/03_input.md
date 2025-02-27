# **Java 筆記**  
## 輸入 Input  

在 Java 中，使用 `Scanner` 類別來讀取使用者輸入  

首先需要 導入 `java.util.Scanner`  
然後建立 `Scanner` 物件來讀取輸入  

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        
    }
}
```

而 `Scanner` 有幾個常見方法  

1. `nextLine()`  
    * 用途：讀取整行字串  
    * 範例：  
        ```java
        String str = scanner.nextLine();
        ```

2. `next()`  
    * 用途：讀取單個單詞  
    * 範例：  
        ```java
        String word = scanner.next();
        ```
        
3. `nextInt()`  
    * 用途：讀取整數  
    * 範例：  
        ```java
        int num = scanner.nextInt();
        ```
        
4. `nextDouble()`  
    * 用途：讀取小數  
    * 範例：  
        ```java
        double pi = scanner.nextDouble();
        ```
        
5. `nextBoolean()`  
    * 用途：讀取布林  
    * 範例：  
        ```java
        boolean isTrue = scanner.nextBoolean();
        ```
        
## 範例  

### 程式碼  
```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("What is your name?");
        String name = scanner.nextLine();

        System.out.println("Age?");
        int age = scanner.nextInt();

        System.out.println("Hello," + name + "! You're " + age + " years old.");

        scanner.close();
    }
}
```

### 輸入  
```
Vincenttainan
20
```

### 輸出  
```
What is your name?
Vincenttainan
Age?
20
Hello,Vincenttainan! You're 20 years old.
```

## 注意  

### 讀取混用  

* `next()`, `nextInt()`, `nextDouble()`, `nextBoolean()`：  
這幾個 `scanner` 的讀取方式是讀取至 ` （空格）` 或者 `\n（換行）`  
如果是 ` （空格）` 會把空格吃掉  
如果是 `\n（換行）` 則會停在換行之前  

* `nextLine()`：  
這個則是讀取至 `\n（換行）`  
並且會把換行吃掉  

因此，如果混合使用 `nextLine()` 與其他幾個的話  
需要注意會不會有額外的 `\n（換行）`  
如果有則需要額外使用一次 `nextLine()` 來消耗 `\n（換行）`  

### 關閉 Scanner  

如果不關閉 `Scanner` （即沒有 `scanner.close();` ）  
程式仍然可以運行，但可能會有以下影響：  

1. 資源洩漏  
`Scanner` 會佔用 系統資源，如果開啟 `Scanner` 但不關閉  
它可能會一直**佔用記憶體**或**未釋放輸入流**，導致資源洩漏  
這通常影響**長時間**運行的程式，例如伺服器應用程式  
但對於**短時間**運行的程式，影響較小  

2. 可能導致 Input Stream 錯誤  
如果使用 `System.in` 來建立 `Scanner`，它會**一直開啟**標準輸入流  
但如果你在一個較大的程式中**多次創建** `Scanner` 而不關閉，可能會發生**程式無法正確讀取輸入**的問題  
