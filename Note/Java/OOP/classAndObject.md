# **Java 筆記**  
## 類別與物件 classAndObject  

## 類別的基本概念  

### 什麼是類別？  

類別（Class）是**物件的藍圖**或**模板**  
定義了物件的屬性（變數）與行為（函式）  

### 什麼是物件？  

物件（Object）是 **類別的實例**  
也就是根據類別創建的具體實體  

### 基本語法  

```java
class Person {
    String name;
    int age;
    
    void sayHello(){
        System.out.println("hello, I am "+name);
    }
}
```

## 建構函式  

### 什麼是建構函式？  

建構函式是一種**特殊的函式**  
在**建立物件**時自動執行  
用來初始化物件的屬性  

### 建構函式的特點  

* 方法名稱與類別名稱相同  
* 沒有回傳值（連 `void` 都不需要）  
* 建立物件時會自動執行  
* 可以有多個建構函式（建構函式多載 `Overloading`）  

### 1. 預設建構函式  

#### 程式碼  
```java
public class Main {
    public static void main(String[] args) {
        Person p=new Person();
        p.intro();
    }
}

class Person {
    String name;
    int age;

    void intro(){
        System.out.println("Name : "+name+"\nAge : "+age);
    }
}
```

#### 輸出  
```
Name : null
Age : 0
```

如果沒有定義建構函式  
Java 會自動提供一個無參數的建構函式  
但它不會做任何初始化工作  

因為沒有初始化  
`String` 預設值為 `null`  
`int` 預設值為 `0`  

### 2. 自訂建構函式  

```java
public class Main {
    public static void main(String[] args) {
        Person p=new Person("Vincenttainan", 19);
        p.intro();
    }
}

class Person {
    String name;
    int age;

    Person(String name, int age){
        this.name=name;
        this.age=age;
    }

    void intro(){
        System.out.println("Name : "+name+"\nAge : "+age);
    }
}
```

#### 輸出  
```
Name : Vincenttainan
Age : 19
```

如果我們希望在建立物件時就給屬性賦值  
就必須自己定義建構函式  

### 3. 多載建構函式  

```java
public class Main {
    public static void main(String[] args) {
        Person p1=new Person("Vincenttainan", 19);
        Person p2=new Person();
        p1.intro();
        p2.intro();
    }
}

class Person {
    String name;
    int age;

    Person(String name, int age){
        this.name=name;
        this.age=age;
    }

    Person(){
        this.name="Unknown";
        this.age=0;
    }

    void intro(){
        System.out.println("Name : "+name+"\nAge : "+age);
    }
}
```

#### 輸出  
```
Name : Vincenttainan
Age : 19
Name : Unknown
Age : 0
```

Java 允許多個建構函式  
只要它們的參數數量或型別不同  

### 4. 在建構函式內呼叫其他建構函式  

```java
public class Main {
    public static void main(String[] args) {
        Person p1=new Person("Vincenttainan", 19);
        Person p2=new Person();
        p1.intro();
        p2.intro();
    }
}

class Person {
    String name;
    int age;

    Person(String name, int age){
        this.name=name;
        this.age=age;
    }

    Person(){
        this("Unknown",0);
    }

    void intro(){
        System.out.println("Name : "+name+"\nAge : "+age);
    }
}
```

#### 輸出  
```
Name : Vincenttainan
Age : 19
Name : Unknown
Age : 0
```

`this()` 用來呼叫本類別的其他建構函式  
這可以避免重複的初始化邏輯  

## `new` 關鍵字  

### `new` 的作用  

`new` 關鍵字用來建立物件  
並在記憶體中分配空間  

這裡的 `new` 也就是前面用了很多次的語法  
