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



123
