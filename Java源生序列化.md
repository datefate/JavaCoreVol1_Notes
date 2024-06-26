## Java 序列化

参考: 

* https://cloud.tencent.com/developer/article/1752784
* 《java core 卷2》第二章

 不要在不受信认的环境中使用java序列化，<font color =red>不推荐使用Java的序列化机制</font>.

### 缺陷： 

*  **易被攻击** ：反序列化过程中容易运行不必要的代码
* **序列化性能太差**
* **序列化后的流太大**
* 无法跨语言

存储一个对象时，这个对象所属的类也必须存储。

 序列化机制有文件输出格式，类似于合同，里面有标识符来表示不同的数据，数据的值，起止符等。
 深究请看 《java core 卷2》第二章
 序列化的重要的应用是，是通过网络将对象传送到另一台计算机上。
 序列化名字由来：与在内存中的存储不同，对象对某个属性的引用在内存中保存的是内存地址
 序列化之后，每个对象都是用一个序列化号保存的。
 序列化算法:

 * 对你遇到的每一个对象引用都关联一个序列号。
 * 对于每一个对象，当第一次遇到时，保存其对象数据到输出流中。
 * 如果某个对象之前已经被保存过，那么只写出“ 与之前保存过的序列号为X的对象相同。 ”
 
 读取对象时，整个过程反过来