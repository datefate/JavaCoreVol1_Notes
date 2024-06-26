



# 《Java核心技术卷一》 笔记 5_2

2019.06.20 15:11



## 第5章 继承（Inheritance）

### 5.3 泛型数组列表

Java 数组虽然可以在运行时动态指定，但是指定大小之后并不能动态更改

解决方案是使用 ArrayList

ArrayList 是一个采用类型参数（type parameter）的泛型类（generic class）



```java
ArrayList<Employee> staff = new ArrayList<Employee>();
ArrayList<Employee> staff = new ArrayList<>(); // since JDK 7
```

使用 add 方法增加元素

```java
staff.add(new Employee());
```

ArrayList 内部靠数组维护，一定次的 add 内部数组满了之后会自动创建更大的数组，并将小数组拷贝过去

可以分配内部数组大小，以免内部的申请空间和拷贝操作

```java
staff.ensureCapacity(100);
```

也可以初始化时指定大小

```java
ArrayList<Employee> staff = new ArrayList<>(100);
```



注意这样分配的空间只是只存储能力，并不是真的有那么多个对象

（这点与申请 100 大小的数组不同）

size 方法返回实际的数组列表元素数量

```java
staff.size()
```



不会添加元素时可以使用 trimToSize 方法释放多余的空间



Java 的 ArrayList 类似于 C++ 的 vector



#### 5.3.1 访问数组列表元素

设置第 i 个元素（从 0 开始）

```java
staff.set(i,harry);
```

set 只能替换已有的元素，添加新元素要使用 add 方法



获取第 i 个元素

```java
Employee e = staff.get(i);
```



可以添加足够的元素之后转为数组

```java
ArrayList<X> list = new ArrayList<>();
while(...) {
    X x ...
    list.add(x);
}
X[] a = new X[list.size()];
list.toArray(a);
```



可以使用带有下标的 add 操作

```java
staff.add(idx, e);
```

可以从中间删除元素

```java
staff.remove(idx);
```



可以使用 for each loop

```java
for(Employee e : staff) ...
```



ArrayListTest.java

```java
import java.time.*;
import java.util.*;

public class ArrayListTest {
	public static void main(String[] args) {
		ArrayList<Employee> staff = new ArrayList<>();

		staff.add(new Employee("Carl Cracker", 75000, 1987, 12, 15)); 
		staff.add(new Employee("Harry Hacker", 50000, 1989, 10, 1));
		//staff.set(2, new Employee("Tony Tester", 40000, 1990, 3, 15));
		// java.lang.IndexOutOfBoundsException
		staff.add(new Employee("Tony Tester", 40000, 1990, 3, 15));

		for(Employee e : staff)
			e.raiseSalary(5);

		for(Employee e : staff)
			System.out.println("name=" + e.getName() + ", salary=" + e.getSalary()
							  + ", hireDay=" + e.getHireDay());
		
		System.out.println("\n===============\n");

		System.out.println(staff.get(0));

		staff.remove(0);
		System.out.println(staff.get(0));

	}
}

class Employee {
	private String name;
	private double salary;
	private LocalDate hireDay;
	public Employee(String n, double s, int year, int month, int day) {
		name = n;
		salary = s;
		hireDay = LocalDate.of(year, month, day);
	}
	public String getName() {
		return name;
	}
	public double getSalary() {
		return salary;
	}
	public LocalDate getHireDay() {
		return hireDay;
	}
	public void raiseSalary(double byPercent) {
		double raise = salary * byPercent / 100;
		salary += raise;
	}

	@Override
	public String toString() {
		return "name = " + name + ", salary = " + salary 
		     + ", hireDay = " + hireDay;
	}
}
```

结果

```text
name=Carl Cracker, salary=78750.0, hireDay=1987-12-15
name=Harry Hacker, salary=52500.0, hireDay=1989-10-01
name=Tony Tester, salary=42000.0, hireDay=1990-03-15

===============

name = Carl Cracker, salary = 78750.0, hireDay = 1987-12-15
name = Harry Hacker, salary = 52500.0, hireDay = 1989-10-01
```



#### 5.3.2 类型化与原始数组列表的兼容性

```java
public EmployeeDB {
    public void update(ArrayList list) {...}
    public78 ArrayList find(String query) {...}
}
```

可以将 类型化的数组列表传递给 update 而不需要类型转换

```java
ArrayList<Employee> staff = ...;
employeeDB.update(staff);
```

编译器没有给出错误信息或者警告。

这样做不是很安全，因为数组列表中的元素可能不是 Employee 的。

对元素进行检索时会发生异常。



```java
ArrayList<Employee> result = employeeDB.find(query);
```

反过来的赋值则会有警告信息（需要增加编译选项 -Xlint:unchecked）

```java
ArrayList<Employee> result = (ArrayList<Employee>)employeeDB.find(query);
```

类型转换也会得到警告信息，指出类型转换有误



出于兼容性考虑，如果确定没有违反规则的现象，可以使用

```
@SuppressWarnings("unchecked")
ArrayList<Employee> result = (ArrayList<Employee>)employeeDB.find(query);
```

取消警告



### 5.4 对象包装器与自动装箱

需要基本类型转换为对象时，每个基本类型有一个跟它相对应的类。

这些对应基本类型的类称为包装器（wrapper）

包装器：

Integer，Long，Float，Double，Short，Byte，Character，Void，Boolean

其中前 6 个派生于 Number。

包装器类的对象是不可变的，一旦创建就不能更改其值。对象包装器还是 final 的，不能定义其子类。

整型数组列表，尖括号中只能使用 Integer 而不能使用 int

int[] 要比 ArrayList\<Integer\> 快得多



自动装箱（autoboxing，autowrapping）

调用

```java
list.add(3);
```

自动装箱为

```java
list.add(Integer.valueOf(3));
```



在赋值给 int 或者算数表达式中会自动拆箱

```java
int n = list.get(i);
Integer n = 3;
n++;
```



注意 == 等号运算符的结果对于基本类型是可预见的

但是对于包装类的比较是不可预见的

boolean，byte，

char <= 127， 

-128 <= short，int <= 127

被包装到固定的对象中



应当使用 equals 对包装类进行判断



包装类变量可能是 null，自动拆箱会 NullPointerException



条件表达式混用 Integer 和 Double ，Integer 拆箱再装箱会提升为 Double 

```java
Integer n = 1;
Double x = 2.0;
System.out.println(true ? n : x); // 1.0
```

拆装箱过程是编译器进行的，不是虚拟机



可以将字符串转化为数字

```java
int x = Integer.parseInt(str);
```



注意 Java 都是按值传递的，因此包装类参数是不能被更改的

```java
public static void triple(int x) // won't work
{
    x = 3 * x;
}
public static void triple(Integer x) // won't work
{
    x = 3 * x;
}
```

在函数内一个新的对象会赋值给 x 但是不会改变传入的参数的引用对象



想修改数值参数值的方法，需要使用 org.omg.CORBA 定义的 holder 类型



IntegerAPI.java

```java
public class IntegerAPI {
    public static void main(String[] args) {
        // java.lang.Integer
        // int intValue()
        // int 形式返回值

        // static String toString(int i)

        // static String toString(int i,int radix)
        // radix 进制下的 i

        // static int parseInt(String s)
        
        // static int parseInt(String s, int radix)
        // 串是 radix 进制的

        // static Integer valueOf(String s)
        // static Integer valueOf(String s, int radix)

        // java.text.NumberFormat
        // Number parse(String s)
        // 返回数字值
    }
}
```



### 5.5 参数数量可变的方法

例如 System.out.printf 就是个参数数量可变的方法

```java
public class PrintStream {
    public PrintStream printf(String fmt, Object... args) {
        return format(fmt, args);
    }
}
```

其中 3 个点的省略号是 Java 代码的一部分，表明方法可以接受任意数量的对象



实际上 printf 接受两个参数，一个是格式字符串，一个是 Object[] 数组

编译器将自动装箱

```java
System.out.printf("%d %s", new Object[] {new Integer(n), "widgets"});
```



可以自定义若干数值的最大值

```java
public static double max(double... value) {
    double largest = Double.NEGATIVE_INFINITY;
    for(double v : values)
        if(v > largest) largest = v;
    return largest;
}
```



甚至可以将 main 定义如下

```java
public static void main(String... args)
```



### 5.6 枚举类

```java
public enum Size {
    SMALL, MEDIUM, LARGE, EXTRA_LARGE
};
```

比较枚举类型的值直接使用 ==

可以使用构造器，将会在构建枚举常量时调用



EnumTest.java

```java
import java.util.*;
public class EnumTest {
    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        System.out.print("Enter a size: (SMALL, MEDIUM, LARGE, EXTRA_LARGE) ");
        String input = in.next().toUpperCase();
        Size size = Enum.valueOf(Size.class, input);
        System.out.println("size = " + size);
        System.out.println("abbreviation = " + size.getAbbreviation());
        if(size == Size.EXTRA_LARGE)
            System.out.println("Good Job");
    }
}

enum Size {
    SMALL("S"), MEDIUM("M"), LARGE("L"), EXTRA_LARGE("XL");

    private String abbreviation;

    private Size(String abbreviation) {
        this.abbreviation = abbreviation;
    }
    public String getAbbreviation() {
        return abbreviation;
    }
}
```

结果1

```text
Enter a size: (SMALL, MEDIUM, LARGE, EXTRA_LARGE) small
size = SMALL
abbreviation = S
```

结果2

```java
Enter a size: (SMALL, MEDIUM, LARGE, EXTRA_LARGE) extra_large
size = EXTRA_LARGE
abbreviation = XL
Good Job
```



EnumAPI.java

```java
public class EnumAPI {
    public static void main(String[] args) {
        // java.lang.Enum <E>
        // static Enum valueOf(Class enumClass, String name)
        // 返回指定 name 给定 enumClass 的枚举常量

        // static E[] values()
        // 返回全部枚举值的数组

        // String toString()
        // 返回枚举常量名，去静态 valueOf 互逆

        // int ordinal
        // 枚举常量声明时的位置，从 0 开始计数

        // int compareTo(E other)
        // 枚举常量出现在 other 之前返回负值，this == other 返回 0，否则返回正值
    }
}
```



简化考虑 Enum 类省略了类型参数，实际上枚举类型 Size 应该扩展为 Enum\<Size\>