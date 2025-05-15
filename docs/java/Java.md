# 📘 Java 首页

---

## 🔢 数组的定义方式（二）：动态初始化数组

```java
数据类型[] 数组名 = new 数据类型[长度];
```

示例：

```java
int[] arr = new int[3];
```

* 动态初始化时，数组中的元素会被自动赋予“默认值”：

  * `int` → `0`
  * `double` → `0.0`
  * `boolean` → `false`
  * `String`（引用类型）→ `null`

---

## 🏗️ 构造器（Constructor）

### 🔹 1. 构造器的定义形式

构造器是一种特殊的方法：

* **没有返回值类型（甚至不能写 `void`）**
* 方法名必须与类名**完全一致**

```java
public class Student {
    // 构造器
    public Student() {
        System.out.println("我是构造方法");
    }
}
```

---

### 🔹 2. 构造器的作用

**Q：构造器什么时候调用？**

* 每次创建对象时都会调用构造器

**Q：构造器常用来做什么？**

* 通常用于**初始化对象的成员变量**

示例：

```java
public class Student {
    String name;

    // 带参的构造器
    public Student(String name) {
        this.name = name; // 使用 this 区分成员变量和参数
    }
}
```

---

## 🔑 this 关键字

`this` 指代当前对象的引用，常用于区分“局部变量”和“成员变量”的冲突。

```java
public class Student {
    String name;

    public Student(String name) {
        this.name = name; // 将传入参数赋值给成员变量
    }
}
```

---

## ⚙️ static 关键字

`static` 表示“静态的”，可以修饰：

* 成员变量（字段）
* 成员方法

### ▶ static 成员变量

* 称为 **类变量**：常用 `类名.变量` 访问
* 同一类的所有对象共享同一个 static 变量

```java
public class Student {
    static String schoolName = "XMU";
}

System.out.println(Student.schoolName);
```

### ▶ 带或不带 static 方法的区别

* **静态方法** 是属于类的，可以直接调用：

```java
public static void printHello() {
    System.out.println("Hello");
}
```

* **实例方法** 需要通过对象来调用，并且可以访问对象的成员变量

```java
public void showName() {
    System.out.println(this.name);
}
```

### ▶ 总结：静态方法 vs 实例方法

| 规则              | 静态方法 (`static`) | 实例方法     |
| --------------- | --------------- | -------- |
| 是否能访问 static 成员 | 可以              | 可以       |
| 是否能访问对象成员       | 不能              | 可以       |
| 是否能用 `this`     | 不能              | 可以       |
| 使用场景            | 通用功能，不依赖对象      | 需要操作对象数据 |

---

## 🧱 面向对象高级语法（OOP）

### 📚 继承（Inheritance）

继承可以：

* 提高代码的复用性，减少重复代码的书写
* 子类可以继承父类的 **非私有成员**（public、protected、default）

语法：

```java
public class SubClass extends SuperClass {
    // 子类扩展功能
}
```

> 子类对象实际上是由“父类部分 + 子类部分”共同组成的。

---

### 🔐 权限修饰符

| 访问修饰符       | 同类 | 同包 | 子类 | 任意类 |
| ----------- | -- | -- | -- | --- |
| `private`   | ✅  | ❌  | ❌  | ❌   |
| *默认*        | ✅  | ✅  | ❌  | ❌   |
| `protected` | ✅  | ✅  | ✅  | ❌   |
| `public`    | ✅  | ✅  | ✅  | ✅   |

---

### 🔁 方法重写（Override）

子类重写（覆盖）父类的方法时需遵守：

1. 方法名、参数列表必须一致。
2. 访问修饰符不能更严格（可以放宽）。
3. 返回类型要相同或是父类返回类型的子类。
4. `private` 和 `static` 方法不能被重写。

**应用场景：** 让对象打印更有意义，比如：

```java
@Override
public String toString() {
    return "Person: name=" + this.name;
}
```

---

### 🧬 子类构造器特点

子类构造器默认会先调用 **父类的无参构造方法**。
如果父类没有无参构造器，子类必须使用 `super(...)` 显式调用父类构造器。

```java
public class Person {
    public Person(String name) { ... }
}

public class Student extends Person {
    public Student(String name) {
        super(name); // 显式调用父类构造器
    }
}
```

---

## 🧠 多态（Polymorphism）

多态是指：**同一个父类引用，在不同子类上表现出不同行为**。

### 多态的前提：

1. 存在继承或实现关系。
2. 父类引用指向子类对象。
3. 子类重写了父类的方法。

### 示例：

```java
Person p = new Student();
 p.run(); // 实际调用的是 Student 重写的 run()
```

> Java 方法是 **动态绑定**，属性不是！

### 多态的限制：

父类引用变量 **不能访问子类独有的方法和属性**：

```java
Person p = new Student();
 p.study(); // ❌ 报错，编译期不可见
```

---

## 🧨 强制类型转换（Downcasting）

当我们需要使用子类的特有功能时，可以**将父类引用强制转换为子类类型**。

```java
Person p = new Student();
Student s = (Student) p;
 s.study(); // ✅ 正常
```

### 注意事项：

* 强制类型转换在编译期不会报错，只要有继承关系就允许转。
* 运行时如果对象的真实类型与目标类型不符，会抛出 `ClassCastException`：

```java
Person p = new Person();
Student s = (Student) p; // ❌ 运行时报错
```

### 安全做法：使用 instanceof 判断

```java
if (p instanceof Student) {
    Student s = (Student) p;
    s.study();
}
```

---

## 🔒 final 关键字

### 定义

`final` 可以修饰**类**、**方法**、**变量**，用于声明“不可变”或“不可被继承/重写”。

### 用法

* **修饰类**：表示该类不能被继承。

  ```java
  public final class Constants { }
  ```
* **修饰方法**：表示该方法不能被子类重写。

  ```java
  public class A {
      public final void doSomething() { ... }
  }
  ```
* **修饰变量**：表示该变量赋值后不能再修改（常量）。

  ```java
  public class B {
      public static final double PI = 3.1415926;
  }
  ```

### 注意事项

* `final` 类不能有子类。
* `final` 方法不能被 override。
* `final` 实例变量必须在声明时或构造器中初始化。
* `final` 局部变量必须在赋值后才能使用。

---

## 📌 常量（Constant）

### 定义

常量是被声明为 `final` 的变量，其值在运行时不会改变。

### 使用场景

* 记录系统配置信息，如文件路径、端口号等。
* 避免“魔法数字”，提高代码可读性和可维护性。

### 优势

* **可读性**：用命名常量替代硬编码值。
* **安全性**：防止意外修改。
* **性能**：JVM 可对 final 常量进行优化（编译期常量内联）。

### 原理

* 编译期常量会被编译器内联到引用它的代码中（常量池）。
* 修改常量值后需要重新编译所有使用方，以保证引用一致。

---

## 🧩 设计模式（Design Patterns）

### 什么是设计模式？

设计模式是被反复验证的**可重用解决方案**，用于解决软件设计中常见的问题。

### 设计模式解决的问题

* 提高代码复用性和可维护性
* 降低模块间耦合度
* 提高系统的灵活性和可扩展性

### 如何使用设计模式？

1. 理解模式的意图、适用场景、结构和优缺点。
2. 根据需求选择合适的模式。
3. 遵循设计模式的类图和示例代码，实现一致性。

---

### 单例模式（Singleton Pattern）

#### 定义

确保一个类**只**能有一个实例，并提供一个全局访问点。

#### 实现方法

##### 饿汉式单例（线程安全）

```java
public class Singleton {
    private static final Singleton INSTANCE = new Singleton();
    private Singleton() {}
    public static Singleton getInstance() {
        return INSTANCE;
    }
}
```

##### 懒汉式单例（线程不安全）

```java
public class Singleton {
    private static Singleton instance;
    private Singleton() {}
    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```

##### 双重检查锁（线程安全懒加载）

```java
public class Singleton {
    private static volatile Singleton instance;
    private Singleton() {}
    public static Singleton getInstance() {
        if (instance == null) {
            synchronized (Singleton.class) {
                if (instance == null) {
                    instance = new Singleton();
                }
            }
        }
        return instance;
    }
}
```

#### 注意事项

* 私有化构造器，防止外部实例化。
* 使用 `volatile` 避免指令重排序导致的线程安全问题。
* 序列化时通过 `readResolve()` 方法确保单例。
* 使用枚举实现单例最为简洁且防止反序列化破坏单例：

  ```java
  public enum SingletonEnum { INSTANCE; }
  ```

#### 应用场景

* 日志管理器、配置管理器、线程池、缓存管理、驱动程序等。

---

你已系统掌握 Java 的基础语法和核心面向对象概念，接下来可以继续学习：

* 抽象类与接口
* Java 异常处理机制
* 集合框架（List、Map、Set）
* Lambda 表达式 & Stream API
* IO 流与文件操作
* 多线程与并发

欢迎继续深入探索 🚀
