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

###### 使用Callable和Future创建线程
  从JAva 5 开始，Java提供了Callable接口，该接口提供了一个call()方法可以作为线程执行体，但call()方法比run()方法功更强大。
  - call()方法可以没有返回值
  - call()方法可以抛出异常

Java 5提供了Future接口来代表Callable接口里call()方法的返回值，并为Future接口提供了一个FutureTask实现类，该实现类实现类Future接口，并实现了Runnable接口--可以作为Thread、
类的target。
  在Future接口里定义了如下几个公共方法来控制它关联的Callable任务。
  - boolean cancel(boolean myInterruptIfRunning)：试图取消该Future里关联的Callable任务。
  - V get()：返回Callable任务里call()方法的返回值。调用该方法将导致程序阻塞，必须等到子线程结束后才会得到返回值。
  - V get(long timeout , TimeUnit unit)：返回Callable任务里call()方法的饭返回值。该方法让程序最多阻塞timeout和unit指定的时间，如果经过指定的时间后Callable任务依然没有返回值，将会抛出TimeoutException异常。
  - boolean isCancelled()：如果在Callable任务正常完成前被取消，则返回true。
  - boolean isDone()：如果Callable任务完成，则返回true。

  > Callable接口有泛型限制，Callable接口里的泛型参类型与call()方法返回值类型相同。而且Callable接口时函数式接口，因此可使用Lambda表达式创建Callable对象。
  > 

创建并启动有返回值的线程的步骤如下：
1. 创建Callable接口的实现类，并实现call()方法，该call()方法将作为线程执行体，且该call()方法有返回值，再创建Callable实现类的实例。从Java 8开始，可以直接使用Lambda表达式创建Callable对象。
2. 使用FutureTask类来包装Callable对象，该FutureTask对象封装了该Callable对象的call()方法的返回值。
3. 使用FutureTask对象作为Thread对象的target创建并启动新进程。
4. 调用FutureTask对象的get()方法来获得子线程执行结束后的返回值。】

```java
import java.util.concurrent.Callable;
import java.util.concurrent.FutureTask;

public class ThirdThread {
    public static void main(String[] args){
        //创建Callable对象
        ThirdThread tr = new ThirdThread();
        //先使用LAmbda表达式创建Callable<Integer>对象
        //使用FutureTask来操作Callalbe对象
        FutureTask<Integer> task = new FutureTask<Integer>((Callable<Integer>)()->{
            int i = 0;
            for(;i<100;i++){
                System.out.println(Thread.currentThread().getName()+ " 的循环变量i的值："+ i);
            }
            //call()方法可以有返回值
            return i;
        });
        for (int i = 0; i< 100;i++){
            System.out.println(Thread.currentThread().getName()
            + " 的循环变量i的值" + i);
            if(i==20){
                //实质还是一Callable对象来床啊金并启动线程的
                new Thread(task,"有返回值的线程").start();
            }
        }
        try{
            System.out.println("子线程的返回值："+ task.get());
        }catch (Exception ex){
            ex.printStackTrace();
        }
    }
}
```
  实现Callable接口与实现Runnable接口并没有太大的差别，只是Callable的call()方法允许声明抛出异常，而且允许带返回值。
  程序最后调用FuntrureTask对象的get()方法来返回call()方法的返回值--该方法将导致主线程被阻塞，直到call()方法结束并返回为止。

###### 创建线程的三种方式对比
  通过继承Thread类或实现Runnable、Callable接口都可以实现多线程，不过实现Runnable接口与实现Callable接口的方式基本相同，只是Callable接口里定义的方法有返回值，可以自己声明抛出异常而已。这两种方式与Thread方式创建多线程的优缺点：
  - 线程类只是实现了Runable接口或Callable接口，还可以继承其他类。
  - 在这种方式下，多个线程可以共享同一个target对象，所以非常适合多个相同的进程来处理同一份资源的情况，从而可以将CPU、代码和数据分开，形成清晰的模型，较好地体现了面向对象地思想。
  - 劣势是，编程稍稍复杂，如果需要访问当前线程，则必须使用Thread.currentThread()方法。

  采用继承Thread类地方式创建多线程地优缺点：
  - 劣势是，因为线程类已经继承了Thread类，所以不能再继承其他父类
  - 优势是，编写简单，如果需要访问当前线程，则无需使用Thread.currentThread()方法，直接施一公this即可获得当前线程。

所以综上所述，一般采用实现Runnable接口、Callable接口地方式来创建多进程。
##### 线程地生命周期 
  在线程地生命周期中，它要经过新建（New）、就绪（Runnable）、运行（Running）、阻塞（Blocked）和死亡（Dead）5种状态。当线程启动以后，CPU需要在多条线程之间切换，于是线程状态也会多次在运行、就绪之间切换。
###### 新建和就绪状态
  当程序使用new关键字创建一个线程之后，该线程就处于新建状态，Java虚拟机为其分配内存，并初始化其成员变量
  当线程对象调用了start()方法之后，该线程处于就绪状态，JAva虚拟机会为其创建方法调用栈和程序计数器，处于这种状态中地线程并没有开始运行，只是表示该线程可以运行了。至于该线程何时喀什运行，取决于JVM里线程调度器地调度。
  > 如果直接调用线程对象地run()方法，系统把线程对象当成一个普通对象，而run()方法也是一个普通对象，而不是线程执行体。
  > 
  调用了线程地run()方法后，该线程已经不再处于新建状态了，不要再次调用线程对象地start()方法。

  > 只能堆处于新建状态地线程调用start()方法，否则将引发IllegalThreadStateException异常。
  > 

：** 底层平台控制，具有一定随机性**

###### 运行和阻塞状态
  如果处于就绪状态地线程获得了CPU，开始执行run()方法的线程执行体，则该线程处于运行状态如果计算机只有一个CPU，那么在任何时刻只有一个线程处于运行状态。
  线程在运行过程中需要被中断，目的是使其他线程获得执行的机会，线程调度的细节取决于底层平台所采用的策略。
  对于抢占式策略的系统而言，系统会给每个可执行的线程一个小时段来处理任务；但该时间段用完后，系统就会剥夺该线程所占用的资源，让其他线程获得执行的机会。
  所有现代的桌面和服务器操作系统都采用抢占式调度策略，但一些小型设备如手机则可能采用协作式调度策略，
  如发生以下情况时，线程将会进入阻塞状态
  - 线程调用sleep()方法主动放弃所占用的处理器资源。
  - 线程调用了一个阻塞式IO方法，在该方法返回之前，该线程被阻塞。
  - 线程试图获得一个同步监视器，但该同步监视器正被其他线程所持有。
  - 线程在等待某个通知（notify）
  - 程序调用了线程的suspend()方法将该线程挂起。但这个方法容易导致死锁，所以应该尽量避免该方法。

  被阻塞的线程会在合适的时候从新进入就绪状态，所以被阻塞的线程的阻塞解除后，必须重新等待线程调度器再次调度它。
  解除阻塞
  - 调用sleep()方法的线程经过了指定时间。
  - 线程调用的阻塞式IO方法已经返回。
  - 线程成功地获得了试图取得的同步监视器。
  - 线程正等待某个通知时，其他线程发出了一个通知。
  - 处于挂起状态的线程被调用了resume()恢复方法。

###### 线程死亡
- run()或call()方法执行完成，线程正常结束
- 线程抛出一个未捕获的Exception或Error
- 直接调用共该线程的stop()方法来结束该线程--该方法容易导致死锁，通常不推荐使用。

> 当主线程结束时，其他线程不受任何影响，并不会随之结束。一旦线程启动起来后，它就拥有和主线程相同的地位，它不会受主线程影响。
>

  为了测试某个线程是否死亡，可以调用线程对象的IsAlive()方法，当线程处于就绪、运行、阻塞三种状态时，方法将返回true；当线程处于新建、死亡两种状态时，该方法返回false。

> 对已经死亡的线程使用start()方法将引发IllegalThreadStateException异常。
> 

##### 控制线程
###### join线程
  当某个程序执行流中调用其他线程的join()方法时，调用线程的join()方法时，调用线程将被阻塞，直到被join()方法加入的join线程执行完成为止。
  join()方法通常由使用线程的程序调用，以将大问题划分成许多小问题，每个小问题分配一个线程。当所有的小问题都得到处理后，再调用主线程来进一步操作。
```java
public class JoinThread extends Thread{
    //提供一个有参数的构造器，用于设置该线程的名字
    public JoinThread(String name){
        super(name);
    }
    //重写run()方法，定义线程执行体
    public void run(){
        for (int i=0; i< 100; i++){
            System.out.println(getName()+ " " + i );
        }
    }
    public static void main(String[] args) throws Exception{
        //启动子线程
        new JoinThread("新线程").start();
        for(int i = 0; i< 100; i++){
            if(i == 20){
                JoinThread jt = new JoinThread("被Join的线程");
                jt.start();
                //main线程调用了jt线程的join()方法，
                //main线程必须等jt线程执行结束后才会向下执行
                jt.join();
            }
            System.out.println(Thread.currentThread().getName()+ " " + i);
        }
    }
}

```
join()方法有如下三种重载形式
- join()：等待被join的线程执行完成。
- join(long millis)：等待被join的线程的时间最长为millis毫秒。如果再millis毫秒内被join的线程还没执行结束，则不再等待。
- join(long millis, int nanos)：等待被join的线程的时间最长为millis毫秒加nanos好微秒。

###### 后台线程
  有一种线程，它是在后台运行的，它的任务是为其他的线程提供服务，这种线程被称为"后台线程（Daemon Thread）"，又称为“守护线程”或“天使线程”。JVM的垃圾回收就是典型的后台线程。
  后台线程特征：前台线程都死亡，后台线程会自动死亡。
  setDaemon(true)方法可以将指定线程设置成后台线程。
  isDaemon()方法可以判断线程是否为后台线程
  > 前台线程创建的子线程默认是前台线程，后台线程创建的子线程默认是后台线程
  >
###### 线程睡眠：sleep
sleep()方法有两种重载形式
- static void sleep(long millis)：让当前正在执行的线程暂停millis毫秒，并进入阻塞状态，该方法收到系统计时器和线程调度器的精度与准确度的影响。
- static void sleep(long millis,int nanos)

# 真鸡儿累
# 布列斯特要塞
# 休息















































# Lambda表达式？

JavaScript是最典型的函数式编程语言。
函数式编程语言提供了一种强大的功能--碧波啊，相比于传统的编程方法有许多优势，闭包是一个可调用的对象，它记录了一些信息，这些信息来源于它的作用域。Java限制提供的最接近闭包的概念便是Lambda表达式，虽然闭包与Lambda表达式之间存在显著区别，但至少Lambda表达式是闭包很好的代替者。
Lambda表达式结构
- 一个Lambda表达式可以有零个或多个参数
- 参数的类型既可以声明，也可以根据上下文来判断
- 所有参数需包含再圆括号内，参数之间用逗号相隔
- 空括号代表参数集为空
- 当只有一个参数，且其类型可推导时，圆括号()可省略。
- Lambda表达式的主题可包含零条或多条语句
- 如果Lambda表达式主题只有一条语句，花括号可省略。匿名函数的返回类型与该主题表达式一致
- 吐过Lambda表达式的主题包含一条以上语句，则表达式必须包含在花括号中。匿名函数的返回类型与代码块的返回类型一致，若没有则为空。