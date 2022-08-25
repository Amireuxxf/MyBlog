---
title: Java知识点-SE篇
tags: 信息技术
description: 知识点整理
top_img: https://cdn.jsdelivr.net/gh/Amireuxxf/PicGo/img/5.png
cover: https://cdn.jsdelivr.net/gh/Amireuxxf/PicGo/img/57.jpg
abbrlink: 9b28f329
date: 2022-08-22 12:05:56
---
# 面向对象特性？

- **封装**

  利用抽象数据类型将数据和基于数据的操作封装在一起，使其构成一个不可分割的独立实体。数据被保护在抽象数据类型的内部，尽可能地隐藏内部的细节，只保留一些对外接口使之与外部发生联系。用户无需知道对象内部的细节，但可以通过对象对外提供的接口来访问该对象。

  优点:

  - 减少耦合: 可以独立地开发、测试、优化、使用、理解和修改
  - 减轻维护的负担: 可以更容易被程序员理解，并且在调试的时候可以不影响其他模块
  - 有效地调节性能: 可以通过剖析确定哪些模块影响了系统的性能
  - 提高软件的可重用性
  - 降低了构建大型系统的风险: 即使整个系统不可用，但是这些独立的模块却有可能是可用的

  - **继承**

  继承实现了  **IS-A**  关系，例如 Cat 和 Animal 就是一种 IS-A 关系，因此 Cat 可以继承自 Animal，从而获得 Animal 非 private 的属性和方法。

  继承应该遵循里氏替换原则，子类对象必须能够替换掉所有父类对象。

  - **多态**

  多态分为编译时多态和运行时多态:

  - 编译时多态主要指方法的重载
  - 运行时多态指程序中定义的对象引用所指向的具体类型在运行期间才确定

  运行时多态有三个条件:

  - 继承
  - 覆盖(重写)
  - 向上转型

# 对equals()和hashCode()的理解?

- **为什么在重写 equals 方法的时候需要重写 hashCode 方法**?

因为有强制的规范指定需要同时重写 hashcode 与 equals 是方法，许多容器类，如 HashMap、HashSet 都依赖于 hashcode 与 equals 的规定。

- **有没有可能两个不相等的对象有相同的 hashcode**?

有可能，两个不相等的对象可能会有相同的 hashcode 值，这就是为什么在 hashmap 中会有冲突。相等 hashcode 值的规定只是说如果两个对象相等，必须有相同的hashcode 值，但是没有关于不相等对象的任何规定。

- **两个相同的对象会有不同的 hash code 吗**?

不能，根据 hash code 的规定，这是不可能的。

# final、finalize 和 finally 的不同之处?

- final 是一个修饰符，可以修饰变量、方法和类。如果 final 修饰变量，意味着该变量的值在初始化后不能被改变。
- Java 技术允许使用 finalize() 方法在垃圾收集器将对象从内存中清除出去之前做必要的清理工作。这个方法是由垃圾收集器在确定这个对象没有被引用时对这个对象调用的，但是什么时候调用 finalize 没有保证。
- finally 是一个关键字，与 try 和 catch 一起用于异常的处理。finally 块一定会被执行，无论在 try 块中是否有发生异常。

# String、StringBuffer与StringBuilder的区别？

第一点: 可变和适用范围。String对象是不可变的，而StringBuffer和StringBuilder是可变字符序列。每次对String的操作相当于生成一个新的String对象，而对StringBuffer和StringBuilder的操作是对对象本身的操作，而不会生成新的对象，所以对于频繁改变内容的字符串避免使用String，因为频繁的生成对象将会对系统性能产生影响。

第二点: 线程安全。String由于有final修饰，是immutable的，安全性是简单而纯粹的。StringBuilder和StringBuffer的区别在于StringBuilder不保证同步，也就是说如果需要线程安全需要使用StringBuffer，不需要同步的StringBuilder效率更高。

# 接口与抽象类的区别？

- 一个子类只能继承一个抽象类, 但能实现多个接口
- 抽象类可以有构造方法, 接口没有构造方法
- 抽象类可以有普通成员变量, 接口没有普通成员变量
- 抽象类和接口都可有静态成员变量, 抽象类中静态成员变量访问类型任意，接口只能public static final(默认)
- 抽象类可以没有抽象方法, 抽象类可以有普通方法；接口在JDK8之前都是抽象方法，在JDK8可以有default方法，在JDK9中允许有私有普通方法
- 抽象类可以有静态方法；接口在JDK8之前不能有静态方法，在JDK8中可以有静态方法，且只能被接口类直接调用（不能被实现类的对象调用）
- 抽象类中的方法可以是public、protected; 接口方法在JDK8之前只有public abstract，在JDK8可以有default方法，在JDK9中允许有private方法

# this() & super()在构造方法中的区别？

- 调用super()必须写在子类构造方法的第一行, 否则编译不通过
- super从子类调用父类构造, this在同一类中调用其他构造均需要放在第一行
- 尽管可以用this调用一个构造器, 却不能调用2个
- this和super不能出现在同一个构造器中, 否则编译不通过
- this()、super()都指的对象,不可以在static环境中使用
- 本质this指向本对象的指针。super是一个关键字
