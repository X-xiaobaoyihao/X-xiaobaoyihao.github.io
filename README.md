<center>
- 👋 Hi, I’m @X-xiaobaoyihao
- ...👀 ...🌱  ...💞️  ...
- 📫 320774407@qq.com
</center>









<center>
<h3>好好学习，天天向上</h3>
</center>


### 6月18日 坚持就是胜利

#### 2021/5/24 星期一 晴  第七天 69.00kg

- 饮食
  - 早餐：两个鸡蛋+青菜包
  - 午餐：青菜+蛋+两碗米饭
  - 晚餐：肉夹馍
  
- 健身
  - 手臂力量
  - 引体向上
  - 腹肌
  
- 学习
  
  - 多线程编程
  
- 总结

  >  好好学习，天天向上

#### 2021/5/25 星期二 晴  第七天 69.90kg

- 饮食

  - 早餐：两个鸡蛋+豆角包
  - 午餐：红萝卜炒肉+青菜
  - 晚餐：鸭血粉

- 健身

  - 篮球
  - 大腿力量
  - 引体向上

- 学习

  - 多线程编程

  - 面试题

    1. ##### 数组和链表的区别

       - 链表通过指针来连接元素与元素，数组则是把所有元素按次序依次存储。
       - 链表的插入、删除元素较为简单，不需要移动数组，且较为容易实现长度扩充，但是寻找某个元素较为困难。
       - 数组寻找某个元素较为简单，但插入与删除比较复杂，由于最大长度需要在编程一开始时指定，故达最大长度时，扩充长度不如链表方便。
       - **相同**
       - 两种结构均可实现数据的顺序存储，构造出来的模型成线性结构。
       - **总结**
       - 数组便于查询和修改，但是不方便新增和删除
       - 链表是适合新增和删除，但是不适合查询，根据业务情况使用和时的数据结构和算法是在大数据量和高并发时必须要考虑的问题。

    2. ##### LinkedList和ArrayList的区别及底层实现

       - LinkedList是基于双向列表的数据结构实现的。

       - ArrayList是基于动态数组实现。

       - **动态数组？**

       - **Array源码分析？**

         首先，ArrayList的继承和实现了类和接口

         ```java
         public class ArrayList<E> extends AbstractList<E>
                 implements List<E>, RandomAccess, Cloneable, java.io.Serializable
         ```

         ArrayList<E>是支持泛型的，所以ArrayList可以构造任何类型的动态数组

         ArrayList继承了AsbstractList抽象类，抽象类实现了很多默认的方法，到那时还有一些方法还是抽线方法。

         实现了通用的List列表接口，这里面定义了List列表的基础方法。

         同时实现了RandomAccess，cloneable,Serializable接口，这三个接口都是空接口，里面没有任何方法声明。

         RandomAccess是一个标记接口，其主要就是提供给List接口用的，用来表明其支持快速随机访问。因为这个接口是没有任何实现的，实现了这个接口的列，就表明这个类支持快速访问，就相当于实现了Serializable就等于支持序列化和反序列化，这个标准。

         Cloneable接口，表明这个是可以进行浅拷贝的，是可以调用Object.clone()返回改对象的浅拷贝。

         **什么是浅拷贝？**

         举个例子：

         假设x是一个非空对象，应该有：

         (x.clone()!=x )==true,也就是说它们不是同一个对象。

         (x.clone().getClass()==x.getClass())==true,也就是它们是同一个类型的class，

         (x.equals(x.clone()))==true,也就是，逻辑上和内容上，它们应该是相同的。

         实现了Cloneable的类应该要满足上面的几个情况。

         **所以ArrayList基础这三个没有定义任何方法定义的接口只是为了表明这个类是支持随机快速访问的，可以支持浅拷贝的，可以被序列化和反序列化的**

         **序列化？**

         ```java
         private transient Object[] elementData;
         ```

         上面这个对象数组就是其存储元素的数据结构，前面有一个java关键字transient，这个关键字是去序列化的意思，即，在这个类序列化后保存到磁盘或者输出到输出流的时候，这个对象数组是不被保存或者输出的。

         这就跟这个ArrayList的特性有关，我们知道ArrayList的容量，也就是这个数组的容量，一般都是预留一些容量，等到容量不够时再拓展，那么就会出现容量还有冗余的情况，如果这时候进行序列化，整个数组都会被序列化，连后面没有意义空元素的也被序列化。这些是不应该被存储的。所以java的设计者，就为这个类提供了一个writeObject方法，在实现了Serializable接口的类，如果这个类提供了writeObject方法，那么在进行序列化的时候就会通过writeObject方法进行序列化，所以ArrayList的writeObject方法就会显式的为每个实际的数组元素进行序列化，只序列化有用的元素。

         ```java
         private void writeObject(java.io.ObjectOutputStream s)
                 throws java.io.IOException{
                 // Write out element count, and any hidden stuff
                 int expectedModCount = modCount;
                 s.defaultWriteObject();
         
         
         
             // Write out array length
             s.writeInt(elementData.length);
         
             // Write out all elements in the proper order.
             for (int i=0; i<size; i++)
                 s.writeObject(elementData[i]);
         
             if (modCount != expectedModCount) {
                 throw new ConcurrentModificationException();
             }
         
         }
         ```

         

    3. ##### Jdk1.7和Jdk中ArrayList有什么区别

- 总结

  > 坚持就是胜利！！！





