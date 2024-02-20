#### 1.一个".java"源文件中是否可以包括多个类（不是内部类）？有什么限制？

​	可以有多个类，但只能有一个public的类，并且public的类名必须与文件名相一致。

#### 2.Java有没有goto?

​	没有，但是 goto 是 java 中的保留字。

#### 3.说说&和&&的区别

​	都表示逻辑与操作，作用是判断两边是否同时为true，只有同时为true时才返回true，否则返回false， &&具有短路与功能， 如果第一个表达式为false， 则直接返回false， &可以进行位运算

#### 4.Java中如何跳出循环

​	break跳出

#### 5.switch

​	switch可以作用于整数和枚举上，整数可以是int也可以是包装类Integer，而且byte， short， char都可以隐式转换为int，所以这些类型或者这些类型的包装类也可以，long不可以， jdk1.7以后，开始支持String类型

#### 6.数据精度转换

​	byte short char int long float double（数据精度从小到大）

##### 	自动类型转换

​		遵循以下规则

​			如果操作数包含Double，其他操作数都转换为Double

​			否则，如果操作数包含float，其他操作数都转换成float

​			否则，如果操作数包含long，其他操作数都转换为long

​			否则，其他操作数都转换为int

​			但是，自动转换职能发生在从精度小的往精度大的转换，否则需要强制转换

​			+=, -+, *=, /= (特殊，编译会强制转换)

##### 	强制类型转换

​			把数据精度高的转换为数据精度低的，double转成int会丢失小数

##### 	隐式强制类型转换

#### 7.String

##### 	String常用API

​	1.charAt(int index) 返回index位置的char

​	2.equals() 如果两个字符串相等，则返回true，否则返回false

​	3.indexOf(char str) 返回str的index下表

​	4.length()返回字符串的长度

​	5.replace(old new)使用new替换成old

​	6.trim()去除空格

​	7.compareTo()只能接受String类型参数

##### 	String，StringBuilder，StringBuffer

​	String底层为final char[]类型的存储结构， final只能被赋值一次，不可变

​	StringBuilder底层为可变对象存储，添加的时候会先检查是否需要扩容，如果需要扩容，则把原来的char[] copy 到一个新的char[] 中， 并把新的char[]的地址给到StringBuilder，扩容为原来的两倍+2的大小

​	StringBuffer为线程安全的，对比StringBuilder，操作方法都多了sync关键字修饰，所以线程安全

###### 	总结：String不可变，StringBuffer线程安全，StringBuilder可变，线程不安全

#### 8.clone（克隆）

​	克隆分为深克隆和浅克隆

##### 	浅克隆

​		是指把内存里的引用复制一份，赋给一个新变量，本质上两个变量都指向同一个内存地址，引用的内容相同，一个变化，另一个也跟着变化

##### 	深克隆

​		是指新建一个空对象，开辟一块内存，然后把原来的对象的数值全部复制过去，完全切断两个对象的联系，互不干扰。

## 9.集合框架

### 		1.collection

​		collection继承Iterable接口，各个实现类去实现各自的迭代器

#### 		1）List

##### 					ArrayList

###### 		ArrayList是如何实现动态增长的？

​			初始化时候，默认容量为0，第一次添加的时候，进行扩容，默认容量为10，后续每次添加的时候会都先判断容量是否足			够，不够的话，调用Arrays.copyOf(该方法实际为system.arrcopy的底层方法，效率高，直接操作内存)进行扩容，扩容成原来大小的1.5倍

###### 		如何在ArrayList中插入和删除元素？它们的效率如何？

​			add插入  

​				头部插入o（n），尾部插入o（1），中间插入o（n）

​			remove()删除

​				删除尾部o（1），删除中间o（n），删除头部o（n）

###### 		什么是ArrayList的扩容机制？它是如何工作的？

###### 		ArrayList和LinkedList的区别是什么？在什么情况下应该使用ArrayList或LinkedList？

​			arraylisy使用数组，linkedlist使用链表，数组随机访问效率高，链表插入删除效率高

###### 		如何使用ArrayList来存储对象？如何比较两个ArrayList是否相等？

​			Arrays.equals（）	

​			.equals

###### 		什么是ArrayList的线程安全问题？如何解决这个问题？

​			Arraylist的迭代器不支持并发修改，在多线程并发修改的时候，会抛出conCurrentModificationException异常

​			可以使用Vector，vector是线程安全的

​			Collections.synchronizedList()可以返回一个线程安全的list

​			JUC提供了线程安全的类例如CopyOnWriteArrayList、ConcurrentLinkedQueue或者集合ConcurrentHashMap、			ConcurrentSkipListMap	

###### 		如何在ArrayList中查找特定的元素？它的效率如何？

​			可以使用ArrayList自带的contains进行查找，该方法会遍历List中所有元素进行匹配，所以效率不高时间复杂度为o（n）

###### 		什么是ArrayList的索引越界异常？如何避免这个异常？

​			在进行获取的时候，获取的索引超出list的大小导致的索引越界，可以使用list.size()确认一下list长度多少

###### 		如何使用ArrayList来存储和处理大数据集合？有哪些优化技巧？

##### 					LinkedList

###### 		什么是LinkedList，它的特点和用途是什么？

​			一个底层由双向链表构成的，双向链表是由一系列结构构成，每个节点都包含数据，指向下一个节点的指针，指向上一个节			点的指针，linkedlist的特点是插入删除速度快。用途是可以实现动态数组，队列，栈等数据结构

###### 		LinkedList是如何实现的，它的底层数据结构是什么？

​			同上

###### 		在LinkedList中插入和删除元素的时间复杂度是多少？

​			插入和删除都是o（1），因为只需要改变指针，不需要移动链表

###### 		如何查找LinkedList中的第n个元素和判断某个元素是否存在？

​			

###### 		如何反转一个LinkedList？

###### 		如何判断一个LinkedList是否有环？	

###### 			快慢指针	

###### 		解释ArrayList和LinkedList的区别，它们各自的优缺点是什么？

###### 		在多线程环境下，如何保证LinkedList的线程安全？

​		

###### 		如何在LinkedList中实现先序、中序和后序遍历？

###### 		给出一个LinkedList的示例代码，实现插入、删除和查找操作。

##### 				Vector

#### 2）Set

##### 					HashSet

##### 		hashset的底层是什么，如何保证元素的唯一性

​			底层也是数组+链表（红黑树），保证唯一性的是通过先计算元素的hashcode，如果出现hash冲突，则调用equals进行比			较，如果equals返回相同，则认定元素冲突，不会插入。

##### 		hashset的特性

​			元素的唯一性

​			元素的无序性

​			允许null的元素

##### 		hashset的插入删除遍历方法

​			add或者addAll

​			remove或者removeAll

​			增强for 迭代器 forEach

##### 					TreeSet

##### 		TreeSet底层

​			底层是通过红黑树实现的红黑树是一种自平衡的二叉查找树，红黑树的特性如下：

​				每个节点是黑色或者是红色

​				跟节点是黑色的

​				每个叶子节点是黑色的

​				如果一个节点是红色的，则他的两个字节点都是黑色的

​				从任一节点到其每个叶子节点的所有简单路径都包含相同数目的黑色节点



#### 3）Queue

​	常见的实现为linkedlist，PriorityQueue，ArrayDeque，

### 2.Map

#### 	hashmap1.7～1.8的优化

##### 		红黑树优化：

​			在 Java 8 中，HashMap 的链表部分在长度达到一定阈值（默认为 8）时会将链表转换为红黑树，以提高在大规模数据情况			下的性能表现。这种改进主要针对解决哈希冲突时的效率问题，对于长度超过阈值的链表，通过转换为红黑树，可以将查找			操作的时间复杂度从 O(n) 降低到 O(log n)。

##### 		数据存储节点的优化：

​			在Java7中，每个节点都是一个单独的对象，需要额外的空间存储只想下一个节点的引用，在Java8中，链表或者红黑树中的			节点中，存储了k-v，并且存储了指向下一个节点的next指针

##### 		头插法改成尾插法：

​			在链表进行插入数据的时候，在并发情况下，多个线程进行插入操作，可能会导致死循环和链表断裂的问题

##### 		扩容先后的问题

​			在Java7中，是先扩容再插入，在Java8中改成了先插入再扩容，然后在进行扩容。

​			原因是Java7中扩容是把所有数据都重新分配到更大的数组中，然后再插入新的数据，这种方式保证了扩容中元素的顺序保			持不变，Java8中由于是使用红黑树进行处理hash冲突，而红黑树的结构不受插入顺序的影响，因此可以先插入后扩容，不			会影响元素的顺序。

#### 	hashmap什么时候会触发扩容

​		hashmap在插入元素的时候，会根据当前元素的数量和负载因子来判断是否需要进行扩容。当元素数量超过负载因子与当前容		量的乘积时，就会触发扩容操作，默认情况下加载因子为0.75

#### 	hashmap在jdk1.8的时候为什么底层换成红黑树

​		在jdk1.7的时候，底层为数组+链表，链表存储，如果大量的数据映射到同一个hash桶内，导致链表挂载的数据过长，会最终导		致hashmap查找元素的时间增长（链表的查找时间复杂度为o（n）），红黑树是一个具有平衡功能的二叉树，其插入删除查找		的时间复杂度均为o（logn），

#### 	hashmap的put过程

​		首先，通过hashcode()方法计算key的hashcode，然后根据hashcode对数组长度进行取模运算，结果就是数组的索引位置，然		后需要判断是否发生hash冲突（根据计算出的索引查看是否有元素，如果有就是，否则不是），则通过链表或者红黑树解决冲		突，否则直接插入k-v，在插入完成后，需要检查是否需要扩容（加载因子X当前容量，如果当前元素数量超过，则需要扩容），		扩容操作具体是新建一个数组，为原来大小的两倍，然后把旧的数组重新进行hash运算挂载到新数组中，插入完成后更新元素		数量并返回值。

#### 	hashmap的get过程

​		首先根据key计算hashcode，然后和hashmap的容量进行取模运算得到index，然后查找是否存在该key，（如果存在hash冲		突，则会查找链表或者红黑树）存在返回value，否则返回null

#### 	hashmap的删除过程

​		根据key进行hash然后与map的大小进行取模运算，得到index，然后找到元素进行删除，删除后判断是否需要缩减大小，如果		需要则缩减为原来的一半，目的是使加载因子保持在一个合理的范围内

#### 	hashmap什么时候会触发扩容

#### 	hashmap的key为空

​		会进行特殊处理，统一放到index为0的下面，hashmap的key和value都可以是null，key只能有一个是null

#### 	hashmap的遍历方式

​		通过迭代器遍历entrySet，map.iterator

​		增强for循环 for（map m ： map） 

​		java8的foreach

#### 10.多线程

#### 	Synchronized

​		作用：

​			原子性：保证同一时间内只有一个线程能够执行同步代码块或者方法

​			可见行：保证共享内存里的数据修改能狗及时可见，这是由JMM内存模型保证的，即在对于一个变量进行unlock时候，需			要把该变量同步到主内存中，对于一个变量进行lock的时候，在使用此变量之前，需要清空工作内存中的这个变量并且从住			内存中重新load一下该变量。

​			有序性：有效解决重排序的问题，即一个unlock操作一定先行发生于后面对同一个锁的lock操作

​		用法：

​			作用于代码块，锁定的是传入的对象

​			作用于方法，实例方法锁的是this（这个实例）（可以简单理解成锁定调用者），静态方法锁的是类

​		原理：

​			

#### 	重排序和happen-before

​		重排序是指Java编译器为了提高性能而对指令执行的顺序进行调整的动作，多线程下可能会影响程序执行的正确性，为了确保多		线程程序的正确性，Java提出了happen-before原则，该原则包括

​			程序顺序规则：在单个线程中，线程内的操作是原来的先后顺序关系，不会发生重排序。

​			监视器锁规则：一个锁的解锁操作对于后续加锁线程是可见的

​			volatile：对一个volitle变量的写操作，对于后续变量的读操作是可见的

​			

#### 11.JUC

#### 12.IO

#### 13.网络编程

#### 14.重载重写

#### 15.public default protected private

#### 16.==&equals

#### 17.final static

#### 18.接口

#### 19.面向对象的特点

#### 20.abstract class  &  interface 区别

#### 21.内部类

#### 22.try catch finally

#### 23.exception体系

#### 24.JDK8新特性

​	1.stream

​	2.Operation

#### 25.序列化

#### 26.反射

#### 27.自定义注解