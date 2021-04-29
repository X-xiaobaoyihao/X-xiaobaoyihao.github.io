<center>
- 👋 Hi, I’m @X-xiaobaoyihao
- ...👀 ...🌱  ...💞️  ...
- 📫 320774407@qq.com
</center>









<center>
<h3>好好学习，天天向上</h3>
</center>





#### 2021/4/22  星期四 小雨
git
MySQL

#### 2021/4/26  星期一 晴
- InnoDB是一个可靠的事务处理引擎，它不支持全文本搜索；
- MEMORY在功能等同于MyISAM，大拿由于数据存储在内存（不是磁盘）中，速度很快（特别适合于临时表）；
- MyISAM是一个性能极高的引擎，它支持全文本搜索，但不支持事务处理。

ISAM(abbr. 索引循环存取法 Index Sequential Access Mode)
事务处理
> **外键不能跨引擎** 混用引擎有一个大缺陷。外键（用于强制实施引用完整性）不能跨引擎，即使使用一个引擎的表不能引用具有使用不同引擎的表的外键。
>

##### 创建存储过程
```mysql
create procedure productpricing()
begin 
	select avg(prod_price) as priceaverage
	from products;
end;
```

##### 建立智能存储过程
```sql
-- Name：
-- Parameters：
--
--
create procedure ordertotal(
 in onumber int,
 in taxable boolean,
 out ototal decimal(8,2)
)
begin
	--
	declare total decimal(8,2);
	declare taxrate int default 6;
	--
	select sum(item_price*quantity)
	from orderitems
	where order_num = onumber
	into total;
	
	if taxable then
		select total+(tatal/100*taxrate) into total;
	end if;
		select total into ototal;
end;
```
# MySql必知必会完结
# Java编程思想
# 深入理解Java虚拟机





#### 2021/4/27  星期二  中雨
java+spring+mysql
研究spring
研究java
研究mysql

# spring



为了降低Java开发的复杂性，Spring采用了以下4种关键策略：
- 基于POKJO的轻量级和最小侵入编程；
- 通过依赖注入和面向接口实现松耦合；
- 通过切面和惯例进行声明式编程；
- 通过切面和模板减少样板代码

DI能够让相互协作的软件组件保持松散耦合，而面向切面编程允许你把遍布应用各处的功能分离出来形成可重用的组件。

AOP能够确保POJO的简单性。

在实际开发种，通常服务器端采用三层体系结构，分别为表现层（web）、业务逻辑层（service）、持久层（dao）。

Spring框架优点
- 方便解耦，简化开发

IOC（控制反转）
DI （依赖注入）
AOP （面向切面编程）



#### 2021/4/29 星期四 晴

#### 第16章 多线程
##### 线程概述
###### 线程和进程
进程是处于运行过程中的程序，并具有一定的独立功能，进程是系统进行资源分配和调度的一个独立单位。
一般而言，进程包含如下三个特征。
- 独立性：进程是系统中独立存在的实体，它可以拥有自己独立的资源，每一个进程都拥有自己私有的地址空间。在没有经过进程本身允许的情况下，一个用户进程不可以直接访问其他进程的地址空间，
- 动态性：进程与程序的区别在于，程序只是一个静态的指令集合，而进程是一个正在系统中活动的指令结合。在进程中加入时间的概念。进程具有自己的生命周期和各种不同的状态。
- 并发性：多个进程可以在单个处理器上并发执行，多个进程之间不会互相影响。

多线程则扩展可多进程的概念，使得同一个进程可以同时并发处理多个任务。线程也被称作轻量级进程，线程是进程的执行单元。线程在程序中是独立的，并发的执行流。
  线程是进程的组成部分，一个进程可以拥有多个线程，一个线程必须有一个父进程。线程可以拥有自己的堆栈、自己的程序计数器和自己的局部变量，但不拥有系统资源，它与父进程的其他线程共享该进程所拥有的全部资源。
  线程是独立允许的，它并不知道进程中是否还有其他线程的存在。线程的执行是抢占式的，也就是说当前运行的线程在任何时候都可能被挂起，以便另一个线程可以运行。
  一个线程可以创建和撤销另一个线程，同一个进程中的多个线程之间可以并发执行。

###### 多线程的优势
  线程在程序中是独立的、并发的执行流，与分隔的进程相比，进程中线程之间的隔离程序要小。它门共享内存、文件句柄和其他每个进程应有的状态。
  因为线程的划分尺度小于进程，使得多线程程序的并发性高。进程在执行过程中拥有独立的内存空间，而多个线程共享内存，从而极大地提高了程序地运行效率。
  线程比进程具有更高的性能，这是由于同一个进程中的线程都有共性--国歌线程共享同一个进程虚拟空间。线程共享的环境包括：进程代码段、进程的共有数据等。利用这些共享的数据，线程很容易实现相互之间的通讯。
  多线程编程具有以下特点：
  - 进程之间不能共享内存，但线程之间共享内存
  - 系统创建进程时需要为该进程重新分配系统资源，但创建线程则代价小得多，因此使用多线程来实现多个任务并发比多进程的效率高。
  - Java语言内置了多线程功能支持，而不是单纯地作为底层操作新系统地调度方式，从而简化了Java的多线程编程

##### 线程的创建和启动
Java使用Thread类代表线程，所有的线程对象都必须是Thread类或其子类的实例。
###### 继承Thread类创建线程类
通过继承Thread类来创建并启动多线程的步骤如下。
1. 定义Thread类的子类，并重写该类的run()方法，该run()方法的方法体就代表了线程需要完成的任务。因此把run()方法称为线程执行体。
2. 创建Thread子类的实例，即创建了线程对象。
3. 调用线程对象的start()方法来启动该线程。
```java
public class FirstThread extends Thread{
    private int i;
    //重写run()方法，run()方法的方法体就是线程执行体
    public void run(){
        for (; i<100;i++){
            //但线程类继承Thread类是，直接使用this即可获得当前线程
            //Thread对象的getName()返回当前线程的名字
            System.out.println(getName() + " " + i);
        }
    }
    public static void main(String[] args){
        for (int i = 0; i < 100; i++){
            //调用Thread的currenetThread().getName()方法来获取当前线程
            System.out.println(Thread.currentThread().getName() +
                    " " + i);
            if (i == 20){
                new FirstThread().start();
                new FirstThread().start();
            }
        }
    }
}
```
当Java程序开始运行后，程序至少会创建一个主线程，主线程的线程执行体不是由run()方法确定的，而是由main()方法确定的--main()方法的方法体代表主线程的线程执行体。
- Thread.currentThread()：currrentThread()是Thread类的静态方法，该方法总是返回当前正在执行的线程对象
- getName()：该方法是Thread类的实例方法，该方法返回调用该方法的线程名字。

> 程序可以通过setName(String name)方法来为线程设置名字，也可以通过getName()方法来返回指定的线程名字。

Thread-0和Thread-1两个线程输出的i变量不连续--注意：i变量是FirstThread的实例变量，而不是局部变量，当应为程序每次创建线程对象时都需要创建一个FirstThread对象，所以Thread-0和Thread-1不能共享该实例变量。
> 使用继承Thread类的方法来创建线程类时，多个线程之间无法共享线程类的实例变量。
> 

###### 实现Runnable接口创建线程类
实现Runnable接口来创建并启动多线程步骤如下：
1. 定义Runnable接口的实现类，并重写该接口的run()方法，该run()方法的方法体同样时该线程的线程执行体。
2. 创建Runnable实现类的实例，并以此实例作为Thread的target来创建Thread对象，该Thread对象才是真正的线程对象。
  > Runable对象仅仅作为Thread对象的target，Runable实现类里包含的run()方法仅作为线程执行体。而实际的线程对象依然时Thread实例，只是改Thread线程负责执行其taraget的run()方法。
  > 

3. 调用线程对象的start()方法来启动该线程。

```java
public class SecondThread implements Runnable{
    private int i;
    @Override
    public void run() {
        for( ; i < 100; i++){
            //当线程类实现Runnable接口时
            //如果想获取当前线程，只能用Thread.currentThread()方法
            System.out.println(Thread.currentThread().getName()
            + " " + i);
        }
    }
    public static void main(String[] args){
        for(int i=0; i< 100; i++){
            System.out.println(Thread.currentThread().getName()+
                    " " + i);
            if(i == 20){
                SecondThread st = new SecondThread();
                new Thread(st, "新线程1").start();
                new Thread(st, "新线程2").start();
            }
        }

    }
}
```
> Runnale接口中只包含一个抽象方法，从Java 8 开始，Runable 接口使用了@FunctionalInterface修饰。也就是说，Runnable接口时函数式接口，可以使用Lambda表达式创建Runable对象。
> 

  ** 从输出结果分析，两个子线程的i变量是连续的，也就是采用Runavle接口的方式创建的多线程可以共享线程类的实例变量。这是因为在这种范式下，程序所创建的Runnable对象只是线程的target，而多线程可以共享一个target，所以多个线程可以共享同一个线程类（实际上因该是线程的target类）的实例变量。**
  
