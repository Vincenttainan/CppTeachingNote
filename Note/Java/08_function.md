# **Java 筆記**  
## 函式 function  

## 1. 基本架構  

```java
[Modifier] [Return Type] [Function Name]([Parameters]){
    // codes here
    return [Return Value];
}
```

* 修飾詞 `[Modifier]`：  
    通常為 `public` 、 `private` 或 `static`  
    這是 物件導向 比較重要的概念，之後會再提  

* 回傳型態 `[Return Type]`：  
    可以是 `int` 、 `double` 、 `String` ，或 `void`（無回傳值）  

* 方法名稱 `[Function Name]`：  
    遵循變數命名規則，通常使用小駝峰命名法  

* 參數列表 `[Parameters]`：  
    可接受的輸入變數（可選）  

* 回傳值 `[Return Value]`：  
    `return` 關鍵字用於回傳值，若為 `void` 則不需要  

## 2. 函式的呼叫  

定義好的方法可以在 `main()` 或其他函式內呼叫  

###  無參數、無回傳值的函式  

#### 程式碼  
```java
public class Main {
    public static void sayHello(){
        System.out.println("Hello, Vincenttainan");
    }

    public static void main(String[] args){
        sayHello();
    }
}
```

#### 輸出  
```
Hello, Vincenttainan
```

### 有參數、無回傳值的方法  

#### 程式碼  
```java
public class Main {
    public static void greet(String str){
        System.out.println("Hello, "+str);
    }

    public static void main(String[] args){
        greet("Vincenttainan");
    }
}
```

#### 輸出  
```
Hello, Vincenttainan
```

### 有參數、有回傳值的方法  

#### 程式碼  
```java
public class Main {
    public static int add(int a, int b){
        return a+b;
    }

    public static void main(String[] args) {
        System.out.println(add(1,2));
    }
}
```

#### 輸出  
```
3
```

### 同名函式重載  

Java 允許同一個方法名稱，根據參數的數量或型態不同來實作多個版本  

#### 程式碼  
```java
public class Main {
    public static int add(int a,int b){
        return a+b;
    }
    public static double add(double a, double b){
        return a+b;
    }
    public static void main(String[] args) {
        System.out.println(add(1,2));
        System.out.println(add(1.1,2.5));
    }
}
```

#### 輸出  
```
3
3.6
```

## 3. `return` 的用法  

函式可以使用 `return` 來回傳一個值，並且立即結束該函式  

### 程式碼  
```java
public class Main {
    public static int add(int a,int b){
        return a+b;
        System.out.println("Vincenttainan");
    }
    public static void main(String[] args) {
        System.out.println(add(1,2));
    }
}
```

### 輸出  
```
Main.java:4: error: unreachable statement
        System.out.println("Vincenttainan");
        ^
1 error
error: compilation failed
```

這邊是因為 `return` 後的程式並無法執行  
所以就 `compile error` 了  

## 4. `static` 函式與非 `static` 函式  

在 `main()` 內直接呼叫的函式需要是 `static`  
因為 `main()` 本身是 `static` 的  

### `static` 函式（靜態方法）  

不需要建立物件就可以直接呼叫的函式，適合工具類函式  

#### 程式碼  
```java
public class Main {
    public static void main(String[] args) {
        System.out.println(Math.add(1,2));
    }
}

public class Math {
    public static int add(int a,int b){
        return a+b;
    }
    public static int time(int a,int b){
        return a*b;
    }
    public static int minus(int a,int b){
        return a-b;
    }
    public static int divide(int a,int b){
        return a/b;
    }
}
```

#### 輸出  
```
3
```

### 非 `static` 函式（靜態方法）  

需要透過物件來呼叫的函式  

#### 程式碼  
```java
public class Main {
    public static void main(String[] args) {
        Person p=new Person();
        p.name="Vincenttainan";
        p.greet("Liz");
    }
}

public class Person {
    String name;
    public void greet(String str){
        System.out.println(name+": hello, "+str);
    }
}
```

#### 輸出  
```
Vincenttainan: hello, Liz
```
