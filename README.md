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


#### 2121/4/30 星期五 晴
  此外Thread还提供了一个与sleep()方法有点相似的yield()静态方法，它可以让正在执行的线程暂停，但它不会阻塞该线程，只是将该线程转入就绪状态。
  当某个线程调用了yield()方法暂停之后，只有优先级与当前线程相同，或者优先级比单钱线程更高的处于就绪状态的线程才会获得执行的机会。
  - sleep()方法暂停当前线程后，会给其他线程执行机会，不会理会其他线程优先级；但yield()方法只会给优先级相同，或优先级更高的线程执行机会。
  - sleep()方法将会线程转入阻塞状态，知道经过阻塞时间才会转入就绪状态；而yield()不会将线程转入阻塞状态，它只是强制当前线程进入就绪状态。
  - sleep()方法声明抛出异常InterruptException异常，所以调用sleep()方法时要么捕捉该异常，要么显式抛出异常；而yield()方法没有声明抛出任何异常。
  - sleep()方法比yield()方法有更好的可移植性，通常不建议施一公yield()方法来控制并发线程的执行。

###### 改变线程优先级
  每个线程的默认优先级都与创建它的父线程的优先级相同，在默认情况下，main线程具有普通优先级，由main线程创建的子线程也具有普通优先级。
  Thread类提供了setPriority（int newPriority）、getPriority()方法来设置和返回指定线程的优先级。
  - MAX_PRIORITY: 10
  - MIN_PRIORITY: 1
  - NORM_PRIORITY: 5

```java
package thread;

public class PriorityTest extends Thread{
    public PriorityTest(String name){
        super(name);
    }
    public void run(){
        for(int i = 0; i < 50; i++){
            System.out.println(getName()+"，其优先级是"
            + getPriority()+",循环变量的值为："+ i);
        }
    }
    public static void main(String[] args){
        Thread.currentThread().setPriority(6);
        for(int i = 0; i < 30; i++){
            if(i == 10){
                PriorityTest low = new PriorityTest("低优先级小线程");
                low.setPriority(Thread.MIN_PRIORITY);
                low.start();
                System.out.println("创建之初的优先级："+low.getPriority());

            }
            if (i == 20){
                PriorityTest high = new PriorityTest("高优先级线程");
                high.setPriority(Thread.MAX_PRIORITY);

                high.start();
            }
        }
    }
}
```

##### 线程同步
# hashCode()和equals()方法重写
>  任何时刻只能有一个线程可以获得对 同步监视器的锁定，当同步代码块完成后，该线程会释放对该同步监视器的锁定。
>  

###### 同步代码块

###### 同步方法 
线程安全的类具有如下特征：
- 该类的对象可以被多个线程安全地访问
- 每个线程调用该对象的人恶化方法之后都将得到正确结果。
- 每个线程调用该对象的 任意方法之后，该对象状态依然保持合理状态。

> synchronized关键字可以修饰代码块，但不能修饰构造器、成员变量等。
> 

  同步方法的同步监视器是this，而this总代表调用该方法的对象。
  可变类的线程安全是以降低程序的运行效率作为代价的，为了减少线程安全所带来的负面影响，程序可采用如下策略。
  - 不要对线程安全类的所有方法都进行同步，只对那些会改变竞争资源的方法进行同步。
  - 如果可变类有两种运行环境：单线程环境和多线程环境，则应该为该可变类提供两种版本，即线程不安全版本和线程安全版本。在单线程环境中使用线程不安全版本以保证性能，在多线程环境中使用线程安全版本。

> JDK所提供的StringBuilder、StringBuffer就是为了照顾单线程环境和多线程环境所提供的类，单线程环境下应该使用StringBuilder来保证较好的性能；当需要保证多线程安全时，就应该使用StringBuffer。
> 

###### 释放同步监视器的锁定
  - 当前线程的同步方法，同步代码块执行结束，当前线程即释放同步监视器。
  - 当前线程在同步代码块、同步方法中遇到break、return终止了该代码块、该方法继续执行，当前线程将会释放同步监视器
  - 当前线程在同步代码块、同步方法中出现了未处理的Error或Exception，导致该代码块、该方法异常结束时，当前线程将会释放同步监视器。
  - 当前线程执行同步代码块或同步方法时，程序执行了同步监视器对象的wait()方法，则当前线程暂停，并释放同步监视器器。
    在如下情况，不会释放同步监视器
  - 线程执行同步代码块或同步方法时，程序调用了Thread.sleep()、Thread.yield()方法来暂停当前线程的执行，当前线程不会释放同步监视器。
  - 线程执行同步代码块时，其他线程调用了该线程的suspend()方法将该线程挂起，该线程不会释放同步监视器。

###### 同步锁（Lock）
###### 死锁
  当两个线程相互等待对象释放同步监视器时就会发生死锁，Java虚拟机没有监测，也没有采取措施来处理死锁情况。

```java
class A{
    public synchronized void foo(B b){
        System.out.println("当前线程名："+Thread.currentThread().getName()
        + "进入了A实例的foo()方法");
        try{
            Thread.sleep(200);
        }catch(InterruptedException ex){
            ex.printStackTrace();
        }
        System.out.println("当前线程名"+ Thread.currentThread().getName()
        + "企图调用B实例的last()方法");
        b.last();
    }
    public synchronized void last(){
        System.out.println("进入了A类的last()方法内部");
    }
}
class B{
    public synchronized void bar(A a){
        System.out.println("当前线程名："+Thread.currentThread().getName()
                + "进入了B实例的bar()方法");
        try{
            Thread.sleep(200);
        }catch(InterruptedException ex){
            ex.printStackTrace();
        }
        System.out.println("当前线程名"+ Thread.currentThread().getName()
                + "企图调用A实例的last()方法");
        a.last();
    }
    public synchronized void last(){
        System.out.println("进入了B类的last()方法内部");
    }
}
public class DeadLock implements Runnable{
    A a = new A();
    B b = new B();
    public void init(){
        //Thread.currentThread().setName("主线程");
        a.foo(b);
        System.out.println("进入了main后");
    }

    @Override
    public void run() {
        //Thread.currentThread().setName("副线程");
        b.bar(a);
        System.out.println("进入了Thread-0后");
    }
    public static void main(String[] args){
        DeadLock dl = new DeadLock();
        new Thread(dl).start();
        dl.init();
    }
}
```
##### 线程通讯

###### 传统的线程通讯
  wait()、notify()和notifyAll()三个方法属于Thread类

# 集合、线程

###### 使用Condition控制线程通讯
###### 使用阻塞队列(BlockingQueue)控制线程通讯
**代码有待思考**输出结果与预期结果不一致，估计是多线程错误可以使用同步方法解决，大概
```java
import com.sun.deploy.util.BlackList;

import java.util.concurrent.ArrayBlockingQueue;
import java.util.concurrent.BlockingQueue;

class Producer extends Thread{
    private BlockingQueue<String> bq;
    public Producer(BlockingQueue<String> bq){
        this.bq = bq;
    }
    public void run(){
        String[] strArr = new String[]{
                "Java",
                "Struts",
                "Spring"
        };
        for (int i = 0; i < 3; i++){
            System.out.println(getName() + "生产者准备生产集合元素！");
            try{
                Thread.sleep(3000);
                bq.put(strArr[i % 3]);
            }catch (Exception ex)
            {
                ex.printStackTrace();
            }
            System.out.println(getName()+"生成完成: " + bq);
        }
    }
}
class Consumer extends Thread{
    private BlockingQueue<String> bq;
    public Consumer(BlockingQueue<String> bq){
        this.bq = bq;
    }
    public void run(){
        while (true){
            System.out.println(getName()+"消费者准备消费集合元素！");
            try{
                Thread.sleep(3000);
                bq.remove();
            }catch (Exception ex){
                ex.printStackTrace();
            }
            System.out.println(getName()+ "消费完成" + bq);
        }
    }
}
public class BlockingQueueTest {
    public static void main(String[] args){
        BlockingQueue<String> bq = new ArrayBlockingQueue<>(1);
        new Producer(bq).start();
        new Producer(bq).start();
        new Consumer(bq).start();
    }
}

```

  使用put()方法尝试放入元素将会阻塞线程；如果使用add()方法尝试放入元素将会引发异常；如果使用offer()方法尝试放入元素将会返回false，元素不会被放入。
  于此类似的是，在BlockingQueue已空的情况下，程序使用take()方法尝试取出元素将会阻塞线程；

##### 线程组和为处理异常
一旦某个线程加入了指定线程组之后，该线程将一直属于该线程组，知道该线程死亡，线程运行中途不能改变它所 属的线程组。
##### 线程池
  线程池在系统启动时即创建大量的空闲的进程，程序将一个Runnable对象或Callable对象传给线程池，线程池在线程池就会启动一个空闲的线程来执行它们的run()或call()方法，当run()或call()方法执行结束之后，该线程并不会死亡，而是再次返回线程池成为空闲状态等待下一个Runnable对象的run()或call()方法。
  除此之外，使用线程池可以有效地控制系统中并发线程的数量，当系统中包含大量并发线程时，会导致系统性能剧烈下降，甚至导致JVM崩溃，而线程池的最大线程数参数可以控制系统中并发线程数不超过此数。
###### Java 8 改进的线程池
# go
#### 2021/5/2 星期天 晴
  在Java 5 以前，开发者必须手动实现自己的线程池；从Java 5 开始，Java内建支持线程池。Java 5新增了一个Exceuteors工厂类来生成线程池，该工厂类包括以下静态工厂方法来创建线程。
  Java 8在线程支持上增加了利用多CPU并行的能力，这样可以更好的发挥底层硬件的性能。
  使用线程池来执行线程任务的步骤如下。
  1. 调用Executors类的静态工厂方法创建一个ExecutorService对象，该对象代表一个线程池。
  2. 创建Runnable实现类或Callable实现类的实例，作为线程执行任务。
  3. 调用ExecutorService对象的submit()方法来提交Runnable实例或Callable实例.
  4. 当不想提交任何任务时,调用ExecutorService对象的shutdown()方法来关闭线程池.

```java
public class ThreadPoolTest {
    public static void main(String[] args) throws Exception{
        //创建一个具有固定线程数(6)的线程池
        ExecutorService pool = Executors.newFixedThreadPool(6);
        //使用Lambda表达式创建Runnable对象
        Runnable target = ()->{
            for ( int i=0; i< 100; i++ ){
                System.out.println(Thread.currentThread().getName()+"的i值为"+i);
            }
        };
        //向线程池中提交两个线程
        pool.submit(target);
        pool.submit(target);
        //关闭线程池
        pool.shutdown();
    }
}
```
###### Java 8增强的ForkJoinPool
  Java 7提供了ForkJoinPool来支持将一个任务拆分成多个"小任务"并行计算,在把多个小任务的结果合并成总的计算结果.ForkJoinPool时ExecutorService的实现类.
  Java 8进一步扩展了ForkJoinPool的功能,Java 8为ForkJoinPool增加了通用池功能.

##### 线程相关类
###### ThreadLocal类
  ThreadLocal,是Thread Local Variable(线程局部变量)的意思,线程局部变量的功能十分简单,就是为没有给使用该变量的线程都提供一个变量值的副本,使每一个线程都可以独立地改变自己的副本,而不会和其他线程的副本冲突。
  - T get()：返回此线程局部变量中当前线程副本中的值。
  - void remove()：删除此线程局部变量中当前线程的值。
  - voidset(T value)：设置此线程局部变量中当前线程副本中的值。

```java
class tlAccount{
    /*
    * 定义一个ThreadLocak类型的变量，该变量将是一个线程局部变量
    * 每个线程都会保留该变量的一个副本
    * */
    private ThreadLocal<String> name = new ThreadLocal<>();

    public ThreadLocal<String> getName() {
        return name;
    }

    public void setName(String name) {
        this.name.set(name);
    }

    //定义一个初始化name成员变量的构造器
    public tlAccount(String str){
        this.name.set(str);
        System.out.println("---"+this.name.get());
    }

}

class MyTest extends Thread{
    //
    private tlAccount account;
    public MyTest(tlAccount account, String name){
        super(name);
        this.account = account;
    }
    public void run(){
        for(int i =0; i<  10; i++){
            if(i==6){
                account.setName(getName());
            }
            System.out.println(account.getName()+"账户i的值"+i);
        }
    }
}
public class ThreadLocalTest {
    public static void main(String[] args){
        tlAccount at = new tlAccount("初始名");
        new MyTest(at ,"线程甲").start();
        new MyTest(at ,"线程乙").start();
    }
}
```
  ThreadLocal和其他所有的同步机制一样，都是为了解决多线程对同一变量的访问冲突。这种情况下，系统并没有将这份资源复制多分，只是采用了安全机制来控制对这份资源的访问。
  ThreadLocal提供了线程安全的共享对象，在编写多线程代码时，可以把不安全的整个变量封装进ThreadLocal，或者把该对象与线程相关的状态使用ThreadLocal保存。

###### 保证线程不安全的集合
  ArrayList、LinkedList、HashSet、TreeSet、HashMap、TreeMap等都是线程不安全的。
  如果程序中有多个线程可能访问以上几个集合，就可以使用Collections提供的方法把这些集合包装成线程安全的集合。Collection提供了如下几个静态方法。

###### 线程安全的集合类
  Java 8扩展了ConcurrentHashMap的功能，Java 8为该类新增了30多个方法，这些方法可以借助于Stream和Lambda表达式支持执行聚集操作。

###### Java 9新增的发布-订阅框架
#### Java集合


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
- 吐过Lambda表达式的主题包含一条以上语句，则表达式必须包含在花括号中。匿名函数的返回类型与代码块的返回类型一致，若没有则为空



#### 2021/5/5 星期三 晴
写作业

校园二手交易平台，写完。good。



![颈椎病康复指南](D:\github\X-xiaobaoyihao.github.io\img\颈椎病康复指南.png)



# next

# 五月目标
#### 1. 尽量向65kg靠拢
#### 2. 看完《疯狂java讲义》、《高性能MySQL》、《spring实战》、《redis设计于实现》
#### 3. 好好学习，天天向上
#### 8.00起床--12.00睡觉
#### 100个上下蹲，100个俯卧撑
#### 奥里给

#### 2021/5/6 星期四 晴
1. JVM垃圾回收算法

  JVM运行时数据区中，线程私有的程序计数器、虚拟机栈、本地方法栈随线程的创建和退出而自动产生和销毁，不需要垃圾回收；而对于方法区和堆区，由于是随虚拟机的启动和退出而创建和销毁，在这期间被各线程共享，若不回收垃圾以腾出空间则最终会耗尽这两部分空间。因此JVM垃圾回收的是共享区域的内存，主要是方法区和Java堆内存的回收。
  **方法区**
  方法区的垃圾收集主要是回收废弃常量和无用的类(卸载类)
  1. 该类的所有实例已被回收，即Java堆中无该类的任何实例（下层）
  2. 该类对应的Java.lang.Class对象没有在任何地方被引用，无在任何地方通过反射访问该类的方法。（下层）
  3. 加载该类的ClassLoader已被回收。(上层)

    java 8提供了-xx:MetaspaceSize来设置出发元空间垃圾回收的阈值。

  #### 什么是OOM？为什么会发生OOM？
  1. OOM含义

    OOM，全程“Out Of Memory”。
  2. 为什么会出现java.lang.OutOfEemoryError:即OOM

    当JVM因为没有足够的内存来为对象分配空间并且垃圾回收期也已经没有空间可回收时，就会抛出java.lang.OutOfMemoryError：
    1. 自身原有：虚拟机本身可用的内存太少
    2. 外在原因：如应用使用的太多，且用完没释放，浪费了内存。此时就会造成内存泄漏或内存溢出。
    **内存泄漏：**申请用完的内存没有释放，导致虚拟机不能再次使用该内存，此时这段内存就泄漏了，因为申请者不用了，而又不能被虚拟机分配给别人用。
    **内存溢出：**申请的内存超出了JVM能提供的内存大小，此时称之为溢出。
  3. OOM的error类型：

    java虚拟机运行时会管理的内存区域：
    1. 程序计数器：当前线程执行的字节码的行号指示器，线程私有
    2. JAVA虚拟机栈：Java方法执行的内存模型，灭个Java方法的执行对应着一个栈帧的进栈和出栈的操作。
    3. 本地方法栈：类似于”JAVA虚拟机栈“，但是为native方法提供内存环境。
    4. JAVA堆：对象内存分配的地方，内存垃圾回收的主要区域，所有线程共享。可分为新生代，老生代。
    5. 方法区：用于存储已经被JVM加载的类信息，常量。静态变量、即编译器编译后的代码等数据。HotSpot中的”永久代“。
    6. 运行时常量池：方法区的一部分，存储常量信息，如各种字面量、符号引用等。
    7. 直接内存：并不是JVM运行时数据区的一部分，可直接访问的内存比如NIO会用到这部分。
    
    所以出了程序计数器不会抛出OOM外，其他各内存区域都可能会抛出OOM。
    常见OOM情况:
    1. java.lang.OutOfMemoryError: Java heap space ------>java堆内存溢出，此种情况最常		见，一般由于内存泄露或者堆的大小设置不当引起。对于内存泄露，需要通过内存监控软件查	找程序中的泄露代码，而堆大小可以通过虚拟机参数-Xms,-Xmx等修改。
    2. java.lang.OutOfMemoryError: PermGen space ------>java永久代溢出，即方法区溢出	了，一般出现于大量Class或者jsp页面，或者采用cglib等反射机制的情况，因为上述情况会产	生大量的Class信息存储于方法区。当出现此种情况时可以通过更改方法区的大小来解决，使用	类似-XX:PermSize=64m -XX:MaxPermSize=256m的形式修改。注意，过多的常量尤其是字符	     串也会导致方法区溢出。
    3. java.lang.StackOverflowError ------> 不会抛OOM error，但也是比较常见的Java内存溢	出。JAVA虚拟机栈溢出，一般是由于程序中存在死循环或者深度递归调用造成的，栈大小设置	      太小也会出现此种溢出。可以通过虚拟机参数-Xss来设置栈的大小。
四、OOM分析

Heap Dump（堆转储文件）它是一个Java进程在某个时间点上的内存快照。Heap Dump是有着多种类型的。不过总体上heap dump在触发快照的时候都保存了java对象和类的信息。通常在写heap dump文件前会触发一次FullGC，所以heap dump文件中保存的是FullGC后留下的对象信息。

通过设置如下的JVM参数，可以在发生OutOfMemoryError后获取到一份HPROF二进制Heap Dump文件： 

-XX:+HeapDumpOnOutOfMemoryError

生成的文件会直接写入到工作目录。  

注意：该方法需要JDK5以上版本。 

转存堆内存信息后，需要对文件进行分析，从而找到OOM的原因。可以使用以下方式：

mat: eclipse memory analyzer, 基于eclipse RCP的内存分析工具。具体使用参考：http://www.eclipse.org/mat/，推荐使用。   

jhat：JDK自带的java heap analyze tool，可以将堆中的对象以html的形式显示出来，包括对象的数量，大小等等，并支持对象查询语言OQL，分析相关的应用后，可以通过http://localhost:7000来访问分析结果。不推荐使用。
#### 垃圾回收


2. 怎么判断对象是否被回收

3. 线程和进程的区别

4. 线程的状态

5. 线程池的工作原理

6. 线程池的七大参数

7. 线程池的状态

8. sleep和wait区别

9. Java如何保证线程安全

10. Redis数据类型

11. Redis缓存雪崩、 穿透、击穿

12. 数据结构

13. 线程池原理、参数、缓存队列

14. mybatis底层源码批量插入item index是什么

15. spring配置文件加载过程，spring源码看过么

16. mvc工作原理

17. springcloud组件源码看过么

18. ArrayList和LinkedList区别？为什么前者查询快，增删改查、后者增删改快查询慢？数据扩容的方式？怎么扩容的

19. 锁用过么

20. HsshMap底层原理

21. JVM模型。GC算法。为什么新生代采用复制算法》老年代不用复制算法？复制的区别？为什么要用CMS、G1区别是什么？

22. SQL优化、优化字段最优选什么类型

23. 左旋右旋？

24. 偏各种底层源码、原理、各为什么？

25. 用过哪些集合List、Set、Map、ArrayList和LinkedList、HashMap的底层原理是怎么扩容的

26. JVM构造

27. 堆栈的区别（结合虚拟机中垃圾回收来说一说）

28. 操作系统部分--内存是如何分配的

29. 线程和进程的区别

30. 聊一聊String类，为什么是Final修饰的

31. HashMap和HashTable的区别

32. Spring IoC的好处

33. hashmap原理

34. hashmap在高并发的情况下会出现什么问题

35. concurrenthashamp是如何保证线程安全的？

36. renntrantlock和Synchronized的区别？

37. ReentrantLock公平锁和非公平锁是如何实现的？

38. 膨胀锁（无锁、偏向锁、轻量级锁、重量级锁）？

39. 线程池的七个参数及其介绍（问到在代码中有没有用到过线程池）

40. jvm运行时数据区及其作用？

41. 三种垃圾回收算法？

42. 垃圾回收器（重点详细介绍了CMS的三次标记和G1回收器）

43. 数据库innodb和myISAM的区别？

44. 数据库的索引一般为什么要设置成自增的整数型？

45. 关注原理

46. 项目从哪里来的

# 《深入理解java虚拟机》
### 第二部分 自动内存管理
#### 第二章 Java内存区域于内存溢出异常
##### 运行时数据区域
![运行时数据区](/img/运行时数据区.png)

##### 对象的创建
  当JAva虚拟机遇到一条字节码new指令时，首先将去检查这个指令的参数是否能在常量池中定位到一个类的符号引用，并检查这个符号引用代表的类是否已被加载、解析和初始化过。如果美哟 那必须先执行相应的类加载过程。
#### JVM内存垃圾回收方法
#### 堆
  Java堆里面存放着几乎所有对象的实例，垃圾收集器对堆进行回收前，首先要做的就是确定哪些对象可以作为垃圾回收。
  JDK 1.2后，JAva对引用概念进行了扩充，将引用分为强引用、软引用、弱引用、虚引用、终引用。
  总的来说，回收的堆对象有两类：
1、有被引用的对象：即被软引用、弱引用、虚引用所引用的对象可能被JVM强制当成垃圾回收。

1、软引用：软引用对象在系统将要发生内存耗尽（OOM）前会被回收。

2、弱引用：弱引用对象只能躲过一次垃圾回收，躲过一次后就被回收。其一个特点是它何时被回收是不可确定的，因为这是由GC运行的不确定性所确定的。

3、虚引用：虚引用对象肯定会被回收，一个对象是否有虚引用完全不会对其生存时间构成影响，也无法通过虚引用来取得一个对象实例，对象被设置成虚引用关联的唯一作用是在对象被垃圾收集时收到一个系统通知。JDK里的实现是 sun.misc.Cleaner。

4、终引用：当对象实现了finalize方法、该方法未被调用过、方法内部该对象又被成员变量引用，则对象不被回收，否则被回收。具体见下面可达性分析。JDK里的实现是Finalizer。

2、无被引用的对象：需要检查哪些对象已死（没被引用），主要有两种算法检测
**引用计数法：**对象有个计数器记录被引用的个数，为0者可被回收。采用此法的有微软的COM技术、使用ActionScript3的python等。此法存在对象间循环引用的问题导致对象不能被回收。
**可达性分析法：**主流Java虚拟机采用此法。选取一系列GC Roots对象组为起点分析引用链确定不可达对象。采用此法的有Java，Lisp等。对不可达的对象，如果其覆盖了finalize()方法并且没被执行郭，则在JVM对之回收前有一次逃过被回收的机会
```java
public class FinalizeEscapeGc {
    private static FinalizeEscapeGc SAVE_HOOK = null;

    public void isAlive(){
        System.out.println("Yes, I'm still alive");
    }

    public static void main(String[] args) throws Exception{
        SAVE_HOOK = new FinalizeEscapeGc();
        SAVE_HOOK = null;
        System.gc();
        Thread.sleep(500);
        if(SAVE_HOOK != null){
            SAVE_HOOK.isAlive();
        }else{
            System.out.println("No, I'm not alive");
        }
        SAVE_HOOK = null;
        System.gc();
        Thread.sleep(500);
        if(SAVE_HOOK != null){
            SAVE_HOOK.isAlive();
        }else{
            System.out.println("No, I'm not alive");
        }
    }

    @Override
    protected void finalize() throws Throwable{
        super.finalize();
        System.out.println("FinalizeEscapeGc finalize invoke...");
        FinalizeEscapeGc.SAVE_HOOK =this;
    }
}
```
#### 2021/5/7 星期五 晴
##### 扫雷项目

#### 2021/5/8 星期六 晴
  创建应用对象之间协作关系的行为通常称为装配(wiring)，这也是依赖注入（DI）的本质。
  Spring提供了三种主要的装配机制：
  1. 在XML中进行显示配置
  2. 在Java中进行显示配置
  3. 隐式的bean发现机制和自动装配

    Spring从两个角度来实现自动化装配：
  1. 组件扫描（component scaning）：Spring会自动发现应用上下文中所创建的bean。
  2. 自动装配（autowiring）：Spring自动满足bean之间的依赖。

    @conponent注解表明该类会作为组件类，并告知Spring要伟这个类创建bean。
    @componentScan注解，默认会扫描与配置类相同的包及这个包下面的所有子包，查找带有@component注解的类。
    通过XML启动组件扫描
    <context:component-scan base-package="包名" />
  ##### 为组件扫描的bean命名
  默认情况下bean的名字为将类名的第一个字母变为小写。
  也可以使用@Component("bean的id名")
  还有另一种为bean命名的方式，这种方式不使用@Componnent注解，而是使用Java依赖注入规范中所提及的@Named注解来为bean设置ID：
  Spring支持将@Named作为Compoent注解的替代方案。两者之间有一些细微的差异，但是在大多数场景中是，它们是可以互换的。
  #设置组件扫描的基础包
  @ComponentScan("基础包名")
  ##### 通过为bean添加注解实现自动装配
  #### 面向切面的spring
  在软件开发中，散布于应用中多处的功能被称为横切关注点（cross-cutting concern）。通常来讲，这些横切关注点从概念上是与应用的业务逻辑相分离的（但是往往会直接嵌入到应用的业务逻辑之中）。把这些横切关注点与业务逻辑分离正好是面向切面编程(AOP)所要解决的问题。
  依赖注入有助于应用对象之间的解耦，而AOP可以实现横切关注点与它们所影响的对象之间解耦。
  日志是应用切面的常见范例，还有声明式事务。安全和、缓存。
  ##### 什么是面向切面编程
  切面能帮助我们模块化关注点。
  横切关注点可以被模块化为特殊的类，这些类被称为切面（aspect）。这样做有两个好处：首先，现在每个关注点都集中在一个地方，而不是分散到多处代码中；其次，服务模块更简洁，因为它们只包含主要关注点（或核心功能）的diamagnetic，而次要关注点的代码被转移到切面中了。
  ##### 定义AOP术语
  通知（advice）、切点（pointcut）和连接点（join point）。
  **进入某个领域之前，必须学会在这个领域该如何说话**
  通知（advice）
  切面的工作被称为通知。
  通知定义了切面是什么以及何时使用。通知还解决了何时执行这个工作。
  Spring切面可以应用5种类型的通知：
  前置通知（before）：在目标方法被调用之前调用通知功能；
  后置通知（After）：在目标方法完成之后调用通知，此时不会关心方法的 输出后是什么；
  返回通知（After-returning）：在目标方法成功执行之后调用通知；
  异常通知（After-throwing）：在目标方法抛出异常后调用通知；
  环绕通知（Around）：通知包裹了被通知的方法，在被通知的方法调用之前和调用之后执行自定义行为。
  连接点（Join Point）
  连接点是应用执行过程种能够插入切面的一个点。切面代码可以利用这些点插入到应用的正常流程之中，并添加新的行为。
  切点（Pointcut）
  切面（Aspect）
  引入（Introductino）
  织入（weaving）
  Spring提供了4种类型的AOP支持：
  基于代理的经典Spring AOP；
  纯POJO切面
  @AspectJ注解驱动的切面；
  注入式AspectJ切面（适用于Spring各版本）。
  **POJO （Plain Ordinary Java Object）简单的Java对象**
  DAO（Data Access Object）数据访问对象

#### 2021/5/9 星期天 晴 母亲节

# 淦
#### 2021/5/10 星期一 晴 热
#### 每日一题
0001两数之和
```java
import java.util.Arrays;
import java.util.HashMap;
import java.util.Map;

/*
  0001求两数之和
 */
public class Solution_1 {
    //暴力法
    public static int[] towSum_1(int[] nums, int target){
        for(int i = 0; i < nums.length-1; i++){
            for(int j = i+1; j < nums.length; j++){
                if(nums[i]+nums[j] == target){
                    return new int[]{i,j};
                }
            }
        }
        return null;
    }
    //利用hashmap
    public static int[] towSum_2(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++){
            if(map.containsKey(target-nums[i])){
                return new int[]{map.get(target-nums[i]),i};
            }
            map.put(nums[i], i);
        }
        return null;
    }

    public static void main(String[] args){
        int[] nums = new int[]{1,2,3,4};
        int target = 4;
        int[] re = towSum_1(nums,target);
        System.out.println(Arrays.toString(re));

        int[] re_2 = towSum_2(nums,target);
        System.out.println(Arrays.toString(re_2));

    }
}
```
0378从字符串中找出第一个没有重复的字符
```java
/*
    0378从字符串中找出第一个没有重复的字符
 */
import java.util.HashMap;

public class Solution_387 {
    //
    public static int firstUniqChar(String s){
        HashMap<Character,Integer> count = new HashMap<>();
        for(int i = 0; i < s.length(); i++){
             char c = s.charAt(i);
             count.put(c, count.getOrDefault(c,0)+1);
        }
        for(int i = 0; i < s.length(); i++){
            if(count.get(s.charAt(i))==1){
                return i;
            }
        }
        return -1;
    }

    public static void main(String[] args){
        String s = "leecodtl";
        System.out.println(firstUniqChar(s));
    }
}
```

0021合并两个有序链表

```java
import java.util.List;

/*
    0021合并两个有序链表
 */
class ListNode{
    int val;
    ListNode next = null;

    ListNode() {}

    ListNode(int val){
        this.val = val;
    }
}

public class Solution_21 {
    //将数组转换为链表
    public static ListNode arrayToListNode(int[] s){
        ListNode head = new ListNode(s[0]);
        ListNode link = head;
        for(int i = 1; i < s.length; i++){
            ListNode temp = new ListNode(s[i]);
            link.next = temp;
            link = temp;
        }
        return head;
    }
    //打印链表
    public static void printLink(ListNode head){
        while (head != null){
                System.out.print(head.val+" ");
                head = head.next;
        }
        System.out.println("");
    }
    //插队法-迭代遍历
    public static ListNode mergeTwoLists(ListNode l1, ListNode l2){
        ListNode prehead = new ListNode(-1);

        ListNode prev = prehead;
        while (l1 != null && l2 != null){
            if(l1.val < l2.val){
                prev.next = l1;
                l1 = l1.next;
            }else{
                prev.next=l2;
                l2 = l2.next;
            }
            prev = prev.next;
        }
        prev.next = l1 == null ? l2 : l1;
        return  prehead.next;
    }

    public static void main(String[] args){
        int[] nums_1 = {1,5,5};
        int[] nums_2 = {2,4,6};
        ListNode l1 = arrayToListNode(nums_1);
        ListNode l2 = arrayToListNode(nums_2);
        ListNode l3 = mergeTwoLists(l1,l2);
        printLink(l1);
        printLink(l2);
        printLink(l3);
    }
}

```

面试题

#### MySQL
##### 事务的基本要素
1. 原子性：事务是一个原子操作单元，其对数据的修改，要么全都执行，要么全都不执行。
2. 一致性：事务开始前和结束后，数据库的完整性约束没有破坏。
3. 隔离性：同一时间，只允许一个事务请求同一数据，不同的事务之间彼此没有任何干扰。
4. 持久性：事务完成后，事务对数据库的所有更新将被保存的数据库，不能回滚。

###### 事务的定义
- Transaction
- 事务：一个最小的不可再分的工作单元；通常一个事务对应一个完整的业务
- 一个完整的业务需要批量的DML(insert、update、delete)语句共同联合完成
- 事务只和DML语句有关，或者说DML语句才有事务。这个和业务逻辑有关，业务逻辑不同，DML语句各个数也不同。

> 以上两台DML语句必须同时成功或失败。最小单元不可再分，当第一条DML语句执行成功后，并不能将底层数据库中的第一个账户的数据修改，只是将操作记录了一下；这个记录是在内存中完成的；当第二条DML语句执行成功后，和底层数据库文件的数据完成同步。若第二条DLM语句执行失败，则清空所有的历史记录操作，要完成以上功能必须借助事务。
> 

###### 关于事务的一些术语
- 开启事务：Start Transaction
- 事务结束：End Transaction
- 提交事务：Commit Transaction
- 回滚事务：Rollback Transaction

###### 事务开启的标志？事务结束的标志？
开启标志
	任何一条DML语句执行，标志事务的开启
结束标志
	提交：成功的结束，将所有DLM语句操作历史记录和底层硬盘数据来一次同步
	回滚：失败结束，将所有的DML语句操作历史记录全部清空。
	
###### 在MySQL中，事务提交与回滚
> 在MySQL中，默认情况下，事务是自动提交的，也就是说，只要执行一条语句就开启了事务，并提交了事务。
> 

**以上自动提交机制是可以关闭的**

###### 事务四大特征之一--隔离性（isolaion）
1. 事务A和事务B之间具有一定的隔离性
2. 隔离性有4各隔离级别
	1. 读未提交：read uncommit
	2. 读已提交：read commit
	3. 可重复读：repeatable read
	4. 串行化：serializable

##### Mysql的存储引擎
1. 