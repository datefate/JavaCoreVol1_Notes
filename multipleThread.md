## 说明

这部分必须看周志明的《Java虚拟机》第三部分、以及《Java Concurrency In Practice》

初级程序员接触不到，Java core 中的这部分不要看，入门看网上的教程、Java se 中API。

下面对现在的我基本没用，如果要看这部分，请顺便查看Mysql的锁

## 线程状态

- New：新创建的线程，尚未执行；
- Runnable：运行中的线程，正在执行run()方法的Java代码；
- Blocked：运行中的线程，因为某些操作被阻塞而挂起；
- Waiting：运行中的线程，因为某些操作在等待中；
- Timed Waiting：运行中的线程，因为执行sleep()方法正在计时等待；
- Terminated：线程已终止，因为run()方法执行完毕。

```ascii
         ┌─────────────┐
         │     New     │
         └─────────────┘
                │
                ▼
┌ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┐
 ┌─────────────┐ ┌─────────────┐
││  Runnable   │ │   Blocked   ││
 └─────────────┘ └─────────────┘
│┌─────────────┐ ┌─────────────┐│
 │   Waiting   │ │Timed Waiting│
│└─────────────┘ └─────────────┘│
 ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─
                │
                ▼
         ┌─────────────┐
         │ Terminated  │
         └─────────────┘
```

`t.join()`等待`t`线程结束后再继续运行

`interrupt()` 中断线程，前提是线程内部捕获了线程中断信号:`while (! isInterrupted()) `

## synchronized

```java
@FunctionalInterface
public interface Runnable {
    /**
     * When an object implementing interface <code>Runnable</code> is used
     * to create a thread, starting the thread causes the object's
     * <code>run</code> method to be called in that separately executing
     * thread.
     * <p>
     * The general contract of the method <code>run</code> is that it may
     * take any action whatsoever.
     *
     * @see     java.lang.Thread#run()
     */
    public abstract void run();
}
```





## Thread 类



**Noted**

> 不要调用Thread类或者Runabele 对象的的run()。直接调用run()，只会在当前线程中，而不会启动新线程(相当于调用了一个普通的Java方法)。应该调用Threa.start().这个方法将创建一个执行run()方法的新线程 。

start方法在检查后,调用 内部的native 方法

```java
// Thread.start()
public synchronized void start() {
        /**
         * This method is not invoked for the main method thread or "system"
         * group threads created/set up by the VM. Any new functionality added
         * to this method in the future may have to also be added to the VM.
         *
         * A zero status value corresponds to state "NEW".
         */
        if (threadStatus != 0)
            throw new IllegalThreadStateException();

        /* Notify the group that this thread is about to be started
         * so that it can be added to the group's list of threads
         * and the group's unstarted count can be decremented. */
        group.add(this);

        boolean started = false;
        try {
            start0();// 真正的创建一个线程执行
            started = true;
        } finally {
            try {
                if (!started) {
                    group.threadStartFailed(this);
                }
            } catch (Throwable ignore) {
                /* do nothing. If start0 threw a Throwable then
                  it will be passed up the call stack */
            }
        }
    }
```

join()

```java
public final synchronized void join(long millis)
    throws InterruptedException {
        long base = System.currentTimeMillis();
        long now = 0;

        if (millis < 0) {
            throw new IllegalArgumentException("timeout value is negative");
        }

        if (millis == 0) {
            while (isAlive()) {
                wait(0);
            }
        } else {
            while (isAlive()) {
                long delay = millis - now;
                if (delay <= 0) {
                    break;
                }
                wait(delay);
                now = System.currentTimeMillis() - base;
            }
        }
    }
```

## ReentrantLock

1、锁是可重入锁，保持有一个计数来跟踪对lock()方法的调用。一个用该锁锁住的方法，可以调用另一个用该锁锁住的方法。

2、一个锁对象可以有一个或多个相关的条件对象。newCondition()方法获得一个条件对象。

```java
reentrantlock.lock();
try{
	临界区
}finally{
	reentrantlock.unlock();
}
```



ReentrantLock (boolean fair)方法构建一个带有公平策略的锁

####  条件对象

被叫做条件变量（conditional variable）



## synchronized

内部锁和条件存在一些限制

>* 不能中断一个正在试图获得锁的线程
>* 试图获得锁时不能设置超时
>* 每个锁仅有单一条件，可能是不够的
>
>



JVM规范定义了几种原子操作：

- 基本类型（`long`和`double`除外）赋值，例如：`int n = m`；（Java Bean 不需要synchronized的原因）
- 引用类型赋值，例如：`List<String> list = anotherList`。

`long`和`double`是64位数据，JVM没有明确规定64位赋值操作是不是一个原子操作，不过在x64平台的JVM是把`long`和`double`的赋值作为原子操作实现的。

但是，如果是多行赋值语句，就必须保证是同步操作，例如：

```java
class Pair {
    int first;
    int last;
    public void set(int first, int last) {
        synchronized(this) {
            this.first = first;
            this.last = last;
        }
    }
}
```




### 守护线程

在守护线程中，编写代码要注意：守护线程不能持有任何需要关闭的资源，例如打开文件等，因为虚拟机退出时，守护线程没有任何机会来关闭文件，这会导致数据丢失。

是指为其他线程服务的线程。在JVM中，所有非守护线程都执行完毕后，无论有没有守护线程，虚拟机都会自动退出。

因此，JVM退出时，不必关心守护线程是否已结束。

如何创建守护线程呢？方法和普通线程一样，只是在调用`start()`方法前，调用`setDaemon(true)`把该线程标记为守护线程：

### 悲观锁& 乐观锁

乐观锁的意思就是乐观地估计读的过程中大概率不会有写入，因此被称为乐观锁。反过来，悲观锁则是读的过程中拒绝有写入，也就是写入必须等待。显然乐观锁的并发效率更高，但一旦有小概率的写入导致读取的数据不一致，需要能检测出来，再读一遍就行。

### 可重入锁

一个线程可多次获取同一个锁

### ReadWriteLock

悲观的读锁，读写锁分开（如果有线程正在读，写线程需要等待读线程释放锁后才能获取写锁，即读的过程中不允许写

- 只允许一个线程写入（其他线程既不能写入也不能读取）；
- 没有写入时，多个线程允许同时读（提高性能）

适合场景：读多，写少

