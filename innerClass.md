## 内部类

Java的设计者意识到多重继承也不是一无是处, 父类和实现的接口有相同签名的方法时，接口的方法会覆盖父类的方法。由此，内部类应运而生

分类：

* 成员内部类（public、protect、priviate、default； static）
* 局部内部类
* 匿名内部类

### 成员内部类

java的非静态内部类可以使用外部类的所有成员方法和变量。这给继承多个类的同名成员并共享带来可能。同时非匿名内部类可以继承一个父类和实现多个接口，因此外部类想要多继承的类可以分别由内部类继承，并进行Override或者直接复用。

```java
class OutclassName {
	class innerclassName{
	}
}
/* 编译结果：
    在该文件下产生2个类：
    OutclassName.class  OutclassName$innerclassName.class
    
    */
    

```



创建使用内部类：
内部类名

### 局部内部类

如果希望访问所在方法的局部变量，那么这个变量必须是final修饰的不可变的变量
<font color = red>从java 8+ 开始，只要局部变量的事实不变，那么final可以省略</font>
原因：
new出来的对象在堆内存中
局部变量是跟着方法走的，在堆内存当中
方法运行结束后，立刻出栈，局部变量会立刻消失
但是new出来的对象会在堆内存中持续存在，直到垃圾回收消失。

eg:methodOuter() 方法调用结束，num变量随之回收；但是内部类Inner还没被GC回收，
可能存在使用，所以，会在方法被弹出堆前拷贝变量num以便使用（if num可变，则不方寻找

```java
public class Outer {

    public void methodOuter(){
        int  num  = 10;
       
        class Inner{
            
            public void methodInner(String[] args) {
                System.out.println(num);
            }
        }
    }

}
```
### 匿名内部类
引入目的：避免因使用抽象类而必须创建抽象类的实现类

匿名内部类的定义格式 :
```
接口名称 对象名 = new 接口名称（）{

...
}；

/*
解析：
1.new 创建对象
2.接口名称就是匿名内部类需要实现的接口
3.{...} 才是匿名内部类的内容
```
`
#### 匿名对象
new 接口名称{ void fuck(){...} }.fuck();
`
NOTE：
1.在创建对象时只能使用一次，重复使用———— 正常定义来使用
2.匿名对象，在调用方法的时候，只能使用一次。



