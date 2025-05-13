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

* **没有返回值类型（甚至不能写 `void`**
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

* **实体方法** 需要通过对象来调用，并且可以访问对象的成员变量

```java
public void showName() {
    System.out.println(this.name);
}
```

### ▶ 总结：静态方法 vs 实体方法

| 规则              | 静态方法 (`static`) | 实体方法     |
| --------------- | --------------- | -------- |
| 是否能访问 static 成员 | 可以              | 可以       |
| 是否能访问对象成员       | 不能              | 可以       |
| 是否能用 `this`     | 不能              | 可以       |
| 使用场景            | 通用功能，不依赖对象      | 需要操作对象数据 |


