## 编译引包

classpath:导入第三方包,可简写cp

~~~java
java -classpath /usr/local/lift/  : algs4.jar HelloWorld
~~~

`:` 为linux下分隔符

`;`为win下分隔符

`cp`后跟包路径，使用`.`表示当前文件路径下

### 使用断言

java -ea *.class