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
    public Person(String name) {
        ...
    }
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

