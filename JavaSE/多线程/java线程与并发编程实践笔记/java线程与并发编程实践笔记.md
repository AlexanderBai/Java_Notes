# 一、第一章    Thread和Runnable

## （一）、Thread和Runnable

​	Thread是Runnable的直接实现类，Thread类为底层操作系统线程体系架构提供一套统一的接口，单个操作系统线程与Thread对象相关联，Runnable通过run()方法为Thread对象的线程提供可执行代码。

### 1、创建对象

#### ①、创建Runnable对象

```
package com.bbg.RunnableAndThread;

/**
 * Created by bbg28 on 2017/10/29.
 */
public class TestRunnable {
    public static void main(String[] args){
    //第一种通过实现Runnable的一个匿名内部类
        Runnable r1=new Runnable() {
            @Override
            public void run() {
                System.out.println("hello from thread1");
            }
        };
        //第二种lambda表达式
        Runnable r2=()->System.out.println("hello from thread2");
       
       r1.run();
        r2.run();
    }
}
```

#### ②、创建Thread对象

```
package com.bbg.RunnableAndThread;

/**
 * Created by bbg28 on 2017/10/29.
 *第一种继承Thread，并重写run方法
 */
public class TestThread extends Thread{
    @Override
    public void run() {
        System.out.println("hello from thread1");
    }

    public static void main(String[] args){
        TestThread testThread=new TestThread();
       testThread.start();

    }
}
```

```
package com.bbg.RunnableAndThread;

/**
 * Created by bbg28 on 2017/10/29.
 *第二种实现Runnable接口，把实现类的对象作文参数传递给Thread的构造函数
 */
public class Test2Thread implements Runnable {
    @Override
    public void run() {
        System.out.println("hello from thread1");
    }
    public static void main(String [] args){
        Test2Thread test2Thread=new Test2Thread();
        new Thread(test2Thread).start();
    }
}

     
```

### 2、获取或设置线程状态

### 3、启动线程

守护线程和非守护线程

```
package com.bbg.RunnableAndThread;

/**
 * Created by bbg28 on 2017/10/29.
 */
public class TestThread extends Thread{
    @Override
    public void run() {
        System.out.println("hello from thread1");
    }

    public static void main(String[] args){
        
        TestThread testThread=new TestThread();
        System.out.println(testThread.isAlive());//判断线程是否处于运行状态
        
        if (testThread.isAlive()==false){
            testThread.isAlive();
        }
        System.out.println(testThread.isDaemon());//判断是否为守护线程
        if (testThread.isDaemon()==false)
            
        System.out.println(testThread.isAlive());
        System.out.println(testThread.isDaemon());
        testThread.start();//启动线程
    }
}
```

## （二）、操作更高级的线程任务

### 1、中断线程

#### ①、void interrupt()：

用于中断调用此方法的Thread对象所关联的线程，当一个线程调用了sleep()方法和join()方法而被阻塞时，线程的中断状态会被清除

#### ②、static boolean interrupted()：

用于验证当前线程是否已中断。且线程的而中断状态会被清除。

#### ③、boolean isInterrupted():

验证线程是否已中断，该线程的状态不受影响。

```
package com.bbg.RunnableAndThread;

/**
 * Created by bbg28 on 2017/10/30.
 */
public class ThreadDemo1 {
    public static void main(String[]args){
        Runnable runnable= () -> {
            String name=Thread.currentThread().getName();
            int count=0;
            while (!Thread.interrupted()){
                System.out.println(name+":"+count);
            }
        };
        Thread threadA=new Thread(runnable);
        Thread threadB=new Thread(runnable);
        threadA.start();
        threadB.start();
        while (true){
            double n=Math.random();
            if (n>=0.49999999&&n<=5.0000001){
                break;
            }
            threadA.interrupt();
            threadB.interrupt();
        }
    }
}
```

### 2、等待线程

主线程会偶尔启动其他线程去操作单调的计算、下载大文件或操作其他一些耗时的任务。这个启动工作线程的线程（主线程）等待工作线程的结果。

#### ①、void join()

无期限等待直至死亡

#### ②、void join(long millis)

死亡之前最多等待millis秒

#### ③、void join(long millis,int nanos)

死亡之前最多等待millis秒nanos纳秒

### 3、、线程睡眠

#### ①、void sleep(long millis)

#### ②、void sleep(long millis，,int nanos)

# 二章 	同步

## （一）、线程中的问题

### 1、竞态条件

当计算的正确性取决于相对时间或者调度器所控制的多线程交叉是，易出现竞态条件。

```
if (a==10)
    b=a/2.0;
    //若a和b是不是局部变量，以上代码在多线程下是有问题的，因为执行if判断和执行b=a/2.0的是两个不同的线程
    //若一条线程执行完if (a==10)，即将要执行 b=a/2.0时被调度器暂停，而调度器恢复了另一线程改变了a的值，
    //当前一条线程恢复时变量b就不会是5.0
    //若a和b是局部变量，每个线程都会有局部变量的拷贝，故不会发生竞态条件
    
public intgetID（）{//read-modify-writer列子
    return counter++；
}

```

### 2、数据竞争

两条或两条以上的线程（在单个应用中）并发地访问同一块内存区域，同时至少有一条是为了写数据，且各个线程对内存的访问没有顺序。

### 3、缓存变量

JVM以及操作系统会协同寄存器或者处理器缓存中缓存变量，而不是依赖于主 存。既每个线程都持有自己变量的拷贝，在写入变量是就是在写入变量的拷贝。

## （二）、同步临界区访问

​	同步是JVM的一个特性，以保证两个个或多线程在并发时不会执行同时同一块临界区，临界区就是必须以串行方式（一次一个线程）访问的一段代码块。

​	同步是通过监听器来实现的，每个java对象都与一个监听器相关联，这样线程就可以通过获取和释放监听器的锁（一个标识）来上锁或解锁。只有一个线程可以次有监听器的锁。

### 1、同步方法（sychronized)

#### ①、同步在类的实列方法时

锁会和调用同步该方法的类的实列对象相关联

```
class ID{
    private static int counter;
    public  synchronized int getID(){
        return counter++;
    }
    ID id=new ID();
    id.getID();//在这里ID的对象和锁相关联，当线程执行getID()方法时，其他线程会等待该线程释放锁
}
```

#### ②、同步在类的方法上时

锁会和调用该方法的类的java.lang.Class对象相关联


    public class ID{
    	private static int counter;
    	public static synchronized int getID(){
        	return counter++;
    	}
    	  ID id=new ID();
        id.getID();//在这里锁会和ID.Class相关联
    }	


### 2、同步代码块

```
synchronized(OBject){//Object是某个对象的引用，锁会和该对象相关联
  /*statment*/
}
```

## （三）、活跃性问题

### 1、死锁

线程1和线程2相互等待互斥持有的资源

```
package com.bbg.RunnableAndThread;
/**
 * Created by bbg28 on 2017/10/30.
 */
public class DeadlockDemo {

    private final Object lock1=new Object();
    private final Object lock2=new Object();

    public void instanceMethod1(){
        synchronized (lock1){
            synchronized (lock2){
                System.out.println("first thread in instanceMethod1");
            }
        }
    }
    public void instanceMethod2(){
        synchronized ( lock2){
            synchronized (lock1){
                System.out.println("first thread in instanceMethod2");
            }
        }
    }

    public static void main( String args[]){
        final DeadlockDemo deadlockDemo=new DeadlockDemo();

        Runnable runnable1= () -> {
            while (true){
                deadlockDemo.instanceMethod1();
                try {
                    Thread.sleep(50);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        };
        Thread threadA=new Thread(runnable1);

        Runnable runnable2= () -> {
            while (true){
                deadlockDemo.instanceMethod2();
                try {
                    Thread.sleep(50);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        };
        Thread threadB=new Thread(runnable2);

        threadA.start();
        threadB.start();

    }
}
```

### 2、活锁

某个线程持续重试一个总是失败的操作

### 3、饿死

某个线程一直被调度器延迟访问某个资源

## （四）、volatile和final

### 1、volatile

被volatile标记的量对其他线程是可见的。每个线程都会访问该变量从主存中的拷贝，而不会直接访问缓存。既一个线程持有一个量，当这个量被某个线程更改后，不需要经过回写到主存中就对其他线程显示更改后的结果。

```
package com.bbg.RunnableAndThread;

/**
 * Created by bbg28 on 2017/11/1.
 */
public class ThreadStoping {
    public static void main(String[] args){
        class StopAbleThread extends Thread{
            private volatile boolean stoped;
            @Override
            public void run() {
                while (!stoped){
                    System.out.println("runing");
                }
            }
            void stopThread(){
                stoped=true;
            }
        }

        StopAbleThread stopableThread=new StopAbleThread();
        stopableThread.start();
        try {
            Thread.sleep(1000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        stopableThread.stopThread();
    }
}
```

### 2、final

以确保不可变的类、对象、量等也保证了上下文中线程的安全。

```
public final class String{
/*statment*/
}
//如String类是不可变得，所以也不可被继承
```

# 三、第三章	等待和通知	

## （一）、等待/通知API

一般用3个wait()、一个notify()和一个notifyAll()来实现线程交互，三者都在一个同步块中被调用。同步块同步的对象和调用三者的对象是一致的。wait()方法在一个while循环中使用。

### 1、wait()

```
synchronized (obj){
while(){
      obj.wait();	
	}
}
```

### 2、notify()

    synchronized (obj){
    	obj.notify;
    }


## （二）、生产者和消费者

# 四、第四章	额外的线程能力

## （一）、线程组

​	一个线程组代表一组线程，一个线程组一也可包含其他线程组，除初识线程外，每个线程组都有一个父线程组。

## （二）、线程局部变量

​	当某个量需要和某个线程关联时，就可以用ThreadLocal类，ThreadLocal实例代表了一个线程局部变量，它为每一个访问线程提供了单独的存储槽。

```
package com.bbg.RunnableAndThread;

/**
 * 为不同的线程关联不同的用户ID
 * Created by bbg28 on 2017/11/4.
 */
public class ThreadLocalDemo {
    private static volatile ThreadLocal<String> UserID =
            new ThreadLocal<>();

    public static void main( String[] args ) {
       Runnable runnable= () -> {
               String name = Thread.currentThread().getName();
               if (name.equals("A"))
                   UserID.set("foxtrot");
               else
                   UserID.set("charlie");
               System.out.println(name+" "+UserID.get());
       };
        Thread threadA = new Thread(runnable);
        threadA.setName("A");

        Thread threadB = new Thread(runnable);
        threadA.setName("B");

        threadA.start();
        threadB.start();

    }
}
```

InheritableThreadLocal是InheritableThreadLocal的子类，可用此类来实现将对象从父线程传到子线程

```
package com.bbg.RunnableAndThread;

import java.awt.*;

/**
 * 将对象一个从父线程传到子线程
 * Created by bbg28 on 2017/11/4.
 */
public class InheritableThreadLocalDemo {
    
    private static final InheritableThreadLocal<Integer> intval=
            new InheritableThreadLocal<>();
    
    public static void main(String [] args){
        
        Runnable runnable= () -> {
            intval.set(new Integer(10));
            Runnable runnable1= () -> {
                Thread thread=Thread.currentThread();
                String name=thread.getName();
                System.out.printf("%s%d%n",name,intval.get());
            };
            Thread threadChild=new Thread(runnable1);
            threadChild.setName("Child");
            threadChild.start();
        };
        new Thread(runnable).start();
        
    }
    
}
```

## （三）、定时器框架类的

在需要单次执行任务或重复任务时就需要要到定时器框架，用于在定时器上下文中控制线程的执行。

### 1、深入Timer

Timer能够在一个后台线程中调度TimerTask用于后续按序执行，Timer也称任务执行线程。

### 2、深入TimerTask

定时任务都是抽象类TimerTask的子类，这些子类实现了Runnable接口，当子类化TimerTask时，需要重写run()方法。

```
package com.bbg.RunnableAndThread;

import java.util.Timer;
import java.util.TimerTask;

/**
 * 以大约1秒的间隔显示当前系统的时间
 * Created by bbg28 on 2017/11/4.
 */
public class TimerDemo {
    public static void main(String[] args){
        TimerTask timerTask=new TimerTask() {
            @Override
            public void run() {
                System.out.println(System.currentTimeMillis());
            }
        };
        Timer timer=new Timer();
        //从指定的时间对指定的任务重复 固定延迟地执行
        timer.schedule(timerTask,0,1000);
    }
}
```

# 五、第五章

# 五、第五章

# 六、第六章

# 七、第七章

# 八、第八章

## 