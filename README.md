当时重看Java core 时，因觉得需要做笔记，为记录而fork。但自己整理完全看心情，算是比较乱，当时主要是重点突出自己不太熟的（熟悉之后还删了，也没在仓库中保存）。至于Java EE的内容，后面采取存在在项目源码中目录下的Note。<br/>

警告Java core一书不适合入门学习


**官方资料**
- [JVM](https://www.javaworld.com/article/3272244/what-is-the-jvm-introducing-the-java-virtual-machine.html?nsdr=true)是执行程序的 Java 平台组件。
- [JRE](https://www.javaworld.com/article/3304858/what-is-the-jre-introduction-to-the-java-runtime-environment.html)是创建 JVM 的 Java 的磁盘部分。
- JDK 允许开发人员创建可由 JVM 和 JRE 执行和运行的 Java 程序。

[官方doc主页](https://docs.oracle.com/en/java/javase/18/)

删除了原作者的书中源代码，换行符改为了LF。notes以外是我当时添加了的

# 《Java核心编程：卷一》笔记
## 按章节笔记目录

### [前言](./notes/Java核心技术卷一0.md)

### [第 1 章 Java 程序设计概述](./notes/Java核心技术卷一1.md)

[1.1 Java程序设计平台](./notes/Java核心技术卷一1.md#11-java程序设计平台)

[1.2 Java “白皮书”的关键术语](./notes/Java核心技术卷一1.md#12-java-白皮书的关键术语)

[1.3 Java applet 与 Internet](./notes/Java核心技术卷一1.md#13-java-applet-与-internet)

[1.4 Java发展简史](./notes/Java核心技术卷一1.md#14-java发展简史)

[1.5 关于 Java 的常见误解](./notes/Java核心技术卷一1.md#15-关于-java-的常见误解)

### [第 2 章 Java 程序设计环境](./notes/Java核心技术卷一2.md)

[2.1 安装 Java 开发工具包（JDK）](./notes/Java核心技术卷一2.md#21-安装-java-开发工具包jdk)

[2.2 使用命令行工具](./notes/Java核心技术卷一2.md#22-使用命令行工具)

[2.3 使用集成开发环境](./notes/Java核心技术卷一2.md#23-使用集成开发环境)

[2.4 运行图形化应用程序](./notes/Java核心技术卷一2.md#24-运行图形化应用程序)

[2.5 构建并运行 applet *](./notes/Java核心技术卷一2.md#25-构建并运行-applet-)

### [第 3 章 Java 的基本程序设计结构](./notes/Java核心技术卷一3_0.md)

[3.1 一个简单的 Java 应用程序](./notes/Java核心技术卷一3_0.md#31-一个简单的-java-应用程序)

[3.2 注释](./notes/Java核心技术卷一3_0.md#32-注释)

[3.3 数据类型](./notes/Java核心技术卷一3_0.md#33-数据类型)

[3.4 变量](./notes/Java核心技术卷一3_0.md#34-变量)

[3.5 运算符](./notes/Java核心技术卷一3_0.md#35-运算符)

[3.6 字符串](./notes/Java核心技术卷一3_1.md#36-字符串)

[3.7 输入输出](./notes/Java核心技术卷一3_1.md#37-输入输出)

[3.8 控制流程](./notes/Java核心技术卷一3_2.md#38-控制流程)

[3.9 大数值](./notes/Java核心技术卷一3_2.md#39-大数值)

[3.10 数组](./notes/Java核心技术卷一3_2.md#310-数组)

### [第 4 章 对象与类](./notes/Java核心技术卷一4_0.md)

[4.1 面向对象程序设计（OOP）概述](./notes/Java核心技术卷一4_0.md#41-面向对象程序设计oop概述)

[4.2 使用预定义类](./notes/Java核心技术卷一4_0.md#42-使用预定义类)

[4.3 用户自定义类](./notes/Java核心技术卷一4_0.md#43-用户自定义类)

[4.4 静态域与静态方法](./notes/Java核心技术卷一4_1.md#44-静态域与静态方法)

[4.5 方法参数](./notes/Java核心技术卷一4_1.md#45-方法参数)

[4.6 对象构造](./notes/Java核心技术卷一4_1.md#46-对象构造)

[4.7 包](./notes/Java核心技术卷一4_2.md#47-包)

[4.8 类路径](./notes/Java核心技术卷一4_2.md#48-类路径)

[4.9 文档注释](./notes/Java核心技术卷一4_2.md#49-文档注释)

[4.10 类设计技巧](./notes/Java核心技术卷一4_2.md#410-类设计技巧)

### [第 5 章 继承（Inheritance）](./notes/Java核心技术卷一5_0.md)

[5.1 类、超类和子类](./notes/Java核心技术卷一5_0.md#51-类超类和子类)

[5.2 Object：所有类的超类](./notes/Java核心技术卷一5_1.md#52-object所有类的超类)

[5.3 泛型数组列表](./notes/Java核心技术卷一5_2.md#53-泛型数组列表)

[5.4 对象包装器与自动装箱](./notes/Java核心技术卷一5_2.md#54-对象包装器与自动装箱)

[5.5 参数数量可变的方法](./notes/Java核心技术卷一5_2.md#55-参数数量可变的方法)

[5.6 枚举类](./notes/Java核心技术卷一5_2.md#56-枚举类)

[5.7 反射（reflective）](./notes/Java核心技术卷一5_3.md#57-反射reflective)

[5.8 继承的设计技巧](./notes/Java核心技术卷一5_3.md#58-继承的设计技巧)

### [第 6 章 接口、lambda 表达式与内部类](./notes/Java核心技术卷一6_0.md)

[6.1 接口](./notes/Java核心技术卷一6_0.md#61-接口)

[6.2 接口示例](./notes/Java核心技术卷一6_0.md#62-接口示例)

[6.3 lambda 表达式](./notes/Java核心技术卷一6_1.md#6.3-lambda-表达式)

[6.4 内部类（inner class）](./notes/Java核心技术卷一6_2.md#64-内部类inner-class)

[6.5 代理（proxy）](./notes/Java核心技术卷一6_3.md#65-代理proxy)

### [第 7 章 异常、断言和日志](./notes/Java核心技术卷一7_0.md)

[7.1 处理错误](./notes/Java核心技术卷一7_0.md#71-处理错误)

[7.2 捕获异常](./notes/Java核心技术卷一7_1.md#72-捕获异常)

[7.3 使用异常机制的技巧](./notes/Java核心技术卷一7_1.md#73-使用异常机制的技巧)

[7.4 使用断言](./notes/Java核心技术卷一7_2.md#74-使用断言)

[7.5 记录日志*](./notes/Java核心技术卷一7_2.md#75-记录日志)

### [第 8 章 泛型程序设计](./notes/Java核心技术卷一8_0.md)

[8.1 为什么要使用泛型程序设计](./notes/Java核心技术卷一8_0.md#81-为什么要使用泛型程序设计)

[8.2 定义简单的泛型类](./notes/Java核心技术卷一8_0.md#82-定义简单的泛型类)

[8.3 泛型方法](./notes/Java核心技术卷一8_0.md#83-泛型方法)

[8.4 类型变量的限定](./notes/Java核心技术卷一8_0.md#84-类型变量的限定)

[8.5 泛型代码和虚拟机](./notes/Java核心技术卷一8_0.md#85-泛型代码和虚拟机)

[8.6 约束与局限性](./notes/Java核心技术卷一8_1.md#86-约束与局限性)

[8.7 泛型类型的继承规则](./notes/Java核心技术卷一8_1.md#87-泛型类型的继承规则)

[8.8 通配符类型](./notes/Java核心技术卷一8_2.md#88-通配符类型)

[8.9 反射和泛型](./notes/Java核心技术卷一8_3.md#89-反射和泛型)

### [第 9 章 集合](./notes/Java核心技术卷一9_0.md)

[9.1 Java 集合框架](./notes/Java核心技术卷一9_0.md#91-Java-集合框架)

[9.2 具体的集合](./notes/Java核心技术卷一9_1.md#92-具体的集合)

[9.3 映射](./notes/Java核心技术卷一9_2.md#93-映射map)

[9.4 视图与包装器](./notes/Java核心技术卷一9_2.md#94-视图与包装器)

[9.5 算法](./notes/Java核心技术卷一9_3.md#95-算法)
