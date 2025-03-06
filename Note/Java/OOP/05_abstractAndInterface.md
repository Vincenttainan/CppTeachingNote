# **Java 筆記**  
## 抽象類別與介面 abstractAndInterface  

### 抽象類別 `abstract`  

#### 什麼是抽象類別？

抽象類別是 **無法被實例化** 的類別  
它的目的是作為基礎類別，讓其他類別繼承並實作其函式  
抽象類別可以包含：  

1. 已實作的函式  
2. 抽象函式（沒有實作的純函式）  

```java
abstract class Animal{
    abstract void eat();
    // 抽象函式，子類別需實做
    void makeSound(){
        System.out.println("Animal's sound");
    }
    // 具體函式，子類別可直接調用
}
```

#### abstract 函式規則：  

1. 抽象方法 **不能** 有實作內容 `{}`  
2. 抽象方法 **只能** 存在於抽象類別中  
3. 子類別繼承抽象類別後，必須 **實作** 所有抽象方法（否則該子類別也要標記為 `abstract`）  

```java
public class Main {
    public static void main(String[] args) {
        Dog aDog=new Dog();
        aDog.makeSound();
        // 繼承的具體函式
        aDog.eat();
        // 子類別實作的函式
    }
}

abstract class Animal{
    abstract void eat();
    void makeSound(){
        System.out.println("Animal's sound");
    }
}

class Dog extends Animal{
    @Override
    void eat(){
        System.out.println("Dog is eating");
    }
    // 子類別實作父類別的抽象函式
}
```

```
Animal's sound
Dog is eating
```

### `abstract` 用途：  

#### 讓不同類別共享相同的基本功能  

抽象類別可以定義通用行為  
讓所有子類別共用相同的程式碼，減少重複  
例如：  
Animal 都有 `eat()` 行為  
`makeSound()` 不同  
    
#### 應用情境：  

當你有一組類別，例如 Dog、Cat  
它們之間有共同行為，`eat()`  
但某些行為需要子類別自己實作，例如 `makeSound()`  
就適合用 **抽象類別**  

```java
abstract class Animal{
    abstract void sound();
    void eat(){
        System.out.println("Animal is eating");
    }
}

class Dog extends Animal{
    @Override
    void sound(){
        System.out.println("Woof, woof");
    }
}

class Cat extends Animal{
    @Override
    void sound(){
        System.out.println("Meow, meow");
    }
}
```

### 介面 `Interface`  

#### 什麼是介面？  

**介面** 是一種完全抽象的類型，只定義函式，不能實作  
類別使用 `implements` 來實作介面的方法  

```java
interface Flyable{
    void fly();
    // 抽象方法（預設為 public 且 abstract）
}
```

#### 範例：  

```java
interface Flyable{
    void fly();
}

class Bird implements Flyable{
    @Override
    public void fly(){
        System.out.println("Bird is flying");
    }
}
```

### 多重介面 `Multiple Interfaces`  

Java 雖然不支持多重繼承，但是可以做到多重介面  

```java
interface Flyable{
    void fly();
}

interface Fightable{
    void fight();
}

class Bird implements Flyable, Fightable{
    @Override
    public void fly(){
        System.out.println("Bird is flying");
    }
    @Override
    public void fight(){
        System.out.println("Bird is fighting");
    }
}
```

### `default` 函式  

在 Java 8 之後，介面可以有 **預設函式**  
允許在介面內提供 **預設的實作**  

```java
interface Flyable{
    void fly();
    default void rest(){
        System.out.println("Resting");
    }
}

class Bird implements Flyable{
    @Override
    public void fly(){
        System.out.println("Bird is flying");
    }
}
```

### 介面的用途  

#### 提供行為規範，確保不同類別都實作某些功能  

介面是一種契約，確保所有實作類別都具備某些功能，但不提供預設實作  

#### 應用情境：  
當你希望不同類別都能有相同的方法（例如「會飛的東西」都要有 fly() 方法）  
但它們彼此沒有繼承關係，就適合用 **介面**  

### `interfaces` 與 `abstract` 類別混合使用  

有時候，我們可以將 **抽象類別** 與 **介面** 搭配使用，來實作更加靈活的設計  

```java
interface Flyable{
    void fly();
}

abstract class Animal{
    abstract void eat();
}

class Bird extends Animal implements Flyable{
    @Override
    public void fly(){
        System.out.println("Bird is flying");
    }
    @Override
    public void eat(){
        System.out.println("Bird is eating");
    }
}
```

## 抽象類別 `Abstract Class` 與 介面 `Interface` 比較表  

|        **項目**        | **抽象類別（Abstract Class）** |       **介面（Interface）**       |
|:----------------------:|:------------------------------:|:---------------------------------:|
|        **目標**        |    讓子類別**共享基本功能**    |   確保不同類別**都有某些功能**    |
|  **可否有具體方法？**  |              可以              |        不行（Java 8 以前）        |
|    **可否有變數？**    |              可以              | 只能有 `public static final` 常數 |
| **是否支援多重繼承？** |             不支援             |               支援                |
|     **適合用在…**      |     具有**共同行為**的類別     |      具有**相同能力**的類別       |
