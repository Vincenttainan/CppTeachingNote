# **Java 筆記**  
## 繼承 inheritance  

### 什麼是繼承？  

繼承是 OOP 中的重要特性之一  
允許 **子類別** 繼承 **父類別** 的屬性與函式  
避免重複程式碼，提高可維護性  

### 1. `extends` 關鍵字  

`extends` 用於讓子類別繼承父類別的成員（變數與函式）  

#### 語法  

```java
class 父類別{
    // 父類別的成員
}

class 子類別 extends 父類別{
    // 子類別可以使用父類別的成員
}
```

#### 範例  

```java
public class Main {
    public static void main(String[] args) {
        Dog d=new Dog();
        d.name="Doggy";
        d.eat();
        d.bark();
    }
}

class Animal{
    String name;
    void eat(){
        System.out.println(name+" is eating.");
    }
}

class Dog extends Animal{
    void bark(){
        System.out.println(name+" is barking.");
    }
}
```

```
Doggy is eating.
Doggy is barking.
```

### 2. 函式覆寫  

子類別可以重新定義父類別的函式，稱為函式覆寫  

函式覆寫的條件：  

1. 函式名稱、參數列表 必須與父類別相同  
2. 回傳型態必須相容  
3. 存取修飾詞不能比父類別更嚴格（但可以更寬鬆）  
4. 需要加上 `@Override` 註解（可選，但推薦）  

#### 範例  

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Dog d=new Dog();
        d.name="Doggy";
        d.eat();
    }
}

class Animal{
    String name;
    void eat(){
        System.out.println(name+" is eating.");
    }
}

class Dog extends Animal{
    @Override
    void eat(){
        System.out.println(name+" is eating meats.");
    }
}
```

#### 輸出  

```
Doggy is eating meats.
```

### 3. `super` 關鍵字  

`super` 用來存取父類別的成員（變數或函式），或呼叫父類別的建構函式  

#### 使用 `super` 呼叫父類別的方法  

```java
public class Main {
    public static void main(String[] args) {
        Dog d=new Dog();
        d.name="Doggy";
        d.eat();
    }
}

class Animal{
    String name;
    void eat(){
        System.out.println(name+" is eating.");
    }
}

class Dog extends Animal{
    @Override
    void eat(){
        super.eat();
        System.out.println(name+" is eating meats.");
    }
}
```

```
Doggy is eating.
Doggy is eating meats.
```

#### 使用 `super` 呼叫父類別的建構函式  

如果父類別有建構函式  
子類別需要在自己的建構函式內呼叫 `super()`  
確保父類別的初始化邏輯被執行  

```java
public class Main {
    public static void main(String[] args) {
        Dog d=new Dog("Doggy");
    }
}

class Animal{
    String name;
    Animal(String str){
        this.name=str;
        System.out.println("Animal constructor called");
    }
}

class Dog extends Animal{
    Dog(String str){
        super(str);
        System.out.println("Dog constructor called");
    }
}
```

```
Animal constructor called
Dog constructor called
```

### 4. `final` 關鍵字與繼承  

#### `final` 函式：  

如果一個函式加上 `final`，則子類別不能覆寫它  
```java
final void show() {...}  
```

#### `final` 類別：  

如果一個類別加上 `final`，則不能被繼承  
```java
final class Animal {...}  
```
