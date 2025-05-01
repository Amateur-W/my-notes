# 3. 面向对象

Java 是一种面向对象的编程语言。  
面向对象编程（Object-Oriented Programming，简称 OOP）是一种以对象为核心进行程序设计的方法。

本节包含以下几个核心概念和实现方式：

- **类**（Class）：定义对象的模板，包含属性和方法。
- **实例**（Instance）：根据类创建的具体对象。
- **方法**（Method）：定义对象可以执行的操作或行为。
---
- **继承**（Inheritance）：子类可以继承父类的属性和方法，提升代码复用性。
- **多态**（Polymorphism）：允许不同类的对象对同一消息作出响应，提高程序灵活性和可扩展性。

## 3.1 面向对象基础

面向对象编程，是一种通过对象的方式，把现实世界映射到计算机模型的一种编程方法。

现实世界中，我们定义了“人”这种抽象概念，而具体的人则是“小明、小红、小军”等一个个具体的人。  所以，“人”可以定义为一个类（class），而具体的人则是实例（instance）。

---

### 💡 class 与 instance 的概念

- `class` 是一种**对象模板**，它定义了如何创建实例，本身就是一种数据类型。
- `instance` 是根据 class 创建的**实例对象**，可以创建多个 instance，每个 instance 类型相同，但各自的属性可以不同。

---

### 🛠️ 定义 class

在 Java 中，创建一个类，例如命名为 `Person`，如下所示：

```java
class Person {
    public String name;
    public int age;
}
```

一个 `class` 可以包含多个字段（field），字段用来描述一个类的特征。  
上面的 `Person` 类中，我们定义了两个字段：
- 一个是 `String` 类型，命名为 `name`；
- 一个是 `int` 类型，命名为 `age`。

因此，通过 `class`，可以将一组数据集合到一个对象上，实现了**数据封装**。

> `public` 是用来修饰字段的，表示该字段可以被外部访问。

---

### 🏠 创建实例

定义了 `class`，只是定义了对象模板，而要根据该模板创建真正的实例，必须使用 `new` 操作符。

`new` 操作符可以创建一个实例，然后，我们需要定义一个引用类型的变量来指向这个实例：

```java
Person ming = new Person();
```

上述代码创建了一个 `Person` 类型的实例，并通过变量 `ming` 指向它。

注意区分：
- `Person ming`：定义了一个 `Person` 类型的变量 `ming`；
- `new Person()`：创建了一个实例；

两者结合，完成了实例化的过程。

---

### ✏️ 访问和操作实例

有了实例参照，我们就可以通过 "变量.字段" 的方式操作实例：

```java
ming.name = "Xiao Ming"; // 对字段 name 赋值
ming.age = 12;           // 对字段 age 赋值

System.out.println(ming.name); // 访问字段 name
```

再创建另一个实例：

```java
Person hong = new Person();
hong.name = "Xiao Hong";
hong.age = 15;

```

每个实例都拥有自己独立的字段，互不影响。

---

### ⚠️ 注意事项

- 一个 Java 源文件可以包含多个类的定义；
- 但**只能定义一个 `public` 类**，且 `public` 类的名称必须与源文件名一致；
- 如果需要定义多个 `public` 类，必须将它们拆分到多个 Java 源文件中。

