
目录
=================

   * [欢迎大家纠错和补充](#欢迎大家纠错和补充)
   * [php](#php)
      * [ngx php-fpm通信](#ngx-php-fpm通信)
      * [php7 特性,优化点](#php7-特性优化点)
      * [hash 结构实现方式](#hash-结构实现方式)
      * [垃圾回收](#垃圾回收)
   * [go](#go)
      * [iota 常量](#iota-常量)
      * [引用类型包含哪些？](#引用类型包含哪些)
      * [interface](#interface)
      * [有哪些方式安全读写共享变量？](#有哪些方式安全读写共享变量)
      * [channel](#channel)
      * [slice](#slice)
         * [数组](#数组)
         * [切片](#切片)
	 * [线程安全](#线程安全)
      * [new 和 make](#new-和-make)
      * [调度器](#调度器)
         * [G-P-M模型](#g-p-m模型)
      * [垃圾回收](#垃圾回收-1)
         * [标记清扫算法](#标记清扫算法)
      * [问题](#问题)
   * [mysql](#mysql)
      * [存储引擎](#存储引擎)
         * [InnoDB vs MyISAM](#innodb-vs-myisam)
            * [事务支持](#事务支持)
            * [表锁差异](#表锁差异)
            * [全文索引](#全文索引)
      * [锁](#锁)
         * [乐观锁 vs 悲观锁](#乐观锁-vs-悲观锁)
            * [乐观锁](#乐观锁)
            * [悲观锁](#悲观锁)
               * [共享锁（读锁）](#共享锁读锁)
               * [独占锁（写锁）](#独占锁写锁)
         * [锁的颗粒度](#锁的颗粒度)
            * [表级锁](#表级锁)
            * [行级锁](#行级锁)
            * [间隙锁](#间隙锁)
            * [什么场景下用表锁](#什么场景下用表锁)
         * [阻塞 vs 死锁](#阻塞-vs-死锁)
      * [索引](#索引)
         * [索引类型](#索引类型)
            * [数据结构角度](#数据结构角度)
               * [B Tree](#btree)
               * [Hash索引](#hash索引)
            * [从逻辑角度](#从逻辑角度)
               * [主键索引](#主键索引)
               * [普通索引](#普通索引)
               * [唯一索引](#唯一索引)
               * [复合索引](#复合索引)
               * [全文索引](#全文索引-1)
         * [使用原则](#使用原则)
         * [聚簇索引和非聚簇索引](#聚簇索引和非聚簇索引)
         * [问题](#问题-1)
         * [优化慢查询](#优化慢查询)
            * [explain 详解](#explain-详解)
               * [id](#id)
               * [select_type](#select_type)
               * [table](#table)
               * [type](#type)
               * [possible_keys](#possible_keys)
               * [Key](#key)
               * [key_len](#key_len)
               * [ref](#ref)
               * [rows](#rows)
               * [Extra](#extra)
      * [事务](#事务)
         * [事务的隔离级别](#事务的隔离级别)
            * [第一类丢失更新（Lost Update）](#第一类丢失更新lost-update)
            * [脏读](#脏读)
            * [不可重复读](#不可重复读)
            * [第二类丢失更新](#第二类丢失更新)
            * [幻读](#幻读)
         * [隔离级别](#隔离级别)
            * [读未提交（Read Uncommitted）](#读未提交read-uncommitted)
            * [读已提交（Read Committed）](#读已提交read-committed)
            * [可重复读（Repeatable Read）](#可重复读repeatable-read)
            * [可串行化（Serializable）](#可串行化serializable)
         * [分布式事务](#分布式事务)
            * [基于可靠消息服务的分布式事务](#基于可靠消息服务的分布式事务)
            * [TCC（两阶段型、补偿型）](#tcc两阶段型补偿型)
      * [sql的优化](#sql的优化)
      * [join on where](#join-on-where)
         * [inner join](#inner-join)
         * [LEFT JOIN](#left-join)
         * [RIGHT JOIN](#right-join)
   * [Redis](#redis)
      * [Redis为什么这么快](#redis为什么这么快)
      * [持久化](#持久化)
         * [快照 RDB](#快照-rdb)
         * [AOF](#aof)
      * [同步机制](#同步机制)
         * [全量同步](#全量同步)
      * [集群](#集群)
         * [分片 Redis Cluster](#分片-redis-cluster)
         * [哨兵 Sentinel](#哨兵-sentinel)
      * [数据淘汰机制](#数据淘汰机制)
      * [题目](#题目)
   * [算法](#算法)
      * [冒泡排序 O(N2)](#冒泡排序-on2)
      * [选择排序](#选择排序)
      * [插入排序](#插入排序)
      * [快速排序](#快速排序)
      * [计数排序](#计数排序)
      * [动态规划](#动态规划)
         * [上台阶问题](#上台阶问题)
      * [二分查找](#二分查找)
      * [hash查找](#hash查找)
      * [加密算法](#加密算法)
   * [linux](#linux)
      * [常用命令](#常用命令)
         * [awk](#awk)
         * [grep](#grep)
   * [网络](#网络)
      * [七层协议](#七层协议)
         * [四层协议](#四层协议)
      * [TCP UDP的区别](#tcp-udp的区别)
      * [TCP的三次握手](#tcp的三次握手)
      * [在浏览器中输入网址之后执行会发生什么？](#在浏览器中输入网址之后执行会发生什么)
   * [操作系统](#操作系统)
      * [进程线程协程](#进程线程协程)
      * [什么是死锁？死锁产生的条件？](#什么是死锁死锁产生的条件)
   * [其他](#其他)
   * [原因](#原因)

# 欢迎大家纠错和补充

# go

## iota 常量
```
const (
	A = iota    //0
	B           //1
	C = "a"     //a
	D           //a
	E = iota    //4
	F           //5
)

func main() {
	fmt.Println(A, B, C, D, E)
	//0 1 a a 4 5
}
```

## 引用类型包含哪些？
- 切片（slice）
- 字典（map）
- 通道（channel）
- 接口（interface）

## interface
```
type person struct {
	name string
}
func main() {
	var i interface{}
	
	//赋值切片
	a := []int{1, 2, 3}
	i = a
	fmt.Println(i)
	//断言切片
	ia, ok := i.([]int)
	fmt.Println(ia, ok)

	//赋值结构体值
	p := person{name: "zhangsan"}
	i = p
	//断言结构体值
	ip, ok := i.(person)
	fmt.Println(ip.name, ok)
}

//赋值结构体引用
var a I
a = &S{Age: 20}	//取地址
fmt.Println(a.Get())

//断言1，转换为S. 
c, ok := a.(*S)	//类型为指针类型
fmt.Println(c.Get(), ok)

//断言2，转换为S. 
switch t := a.(type) {	//类型为指针类型
case *S:
	fmt.Println(t.Get())
}
```

## 有哪些方式安全读写共享变量？
- 加Mutex锁
- Goroutine 通过 channel 进行安全读写共享变量。
- Goroutine 通过 atomic进行安全读写共享变量。

## channel
```
nil状态 (var c chan int)
input<-: 阻塞,在主线程里调用会引发fatal error deadlock
<-output: 阻塞,在主线程里调用会引发fatal error deadlock
range/select:同output
close : panic: close of nil channel

open状态 (c := make(chan int))
input<-: 正常，阻塞等待输入
<-output: 正常，阻塞等待输出
range/select: 同output
close: 正常

close状态
input<-: panic:send on closed channel
<-output: 正常，都输出类型的初始值（int:0,string:空）
range/select: 同output
close: panic:send on closed channel

作为接受者的goroutine不要关闭channel,对于不再使用的通道不必显示关闭。如果没有goroutine引用这个通道，这个通道就会被垃圾回收。
```


## slice

### 数组
1. 数组是具有固定长度且拥有零个或者多个相同数据类型元素的序列。  
2. 数组的长度是数组类型的一部分，所以不同长度的数组是两种不同的类型。
3. 数组需要指定大小，不指定也会根据初始化的自动推算出大小，且不可改变。
4. 数组是值传递。

### 切片
1. 切片表示一个拥有相同类型元素的可变长度的序列。
2. 切片是一种轻量级的数据结构，它有三个属性：指向底层数组的指针、长度和容量。
3. 切片不需要指定大小。
4. 切片是地址传递。
5. 切片可以通过数组来初始化，也可以通过内置函数 make() 初始化，初始化时长度和容量相等，在追加元素时如果容量不足时将自动扩容。
6. rang遍历数组，切片，map时，都是值拷贝，在循环中更改值不会影响原来的

扩容方式:
1. 当向切片中添加数据时,如果没有超过容量,直接添加
2. 当新增后的长度大于当前容量，小于1024个长度，新的容量是当前容量的2倍。
3. 当新增后长度大于1024，容量循环增加当前容量的四分之一。直到大于新增后的长度。

```
slice = make([]int64, len, cap)

//注意: [startIndex:endIndex]. 
0. 0 <= startIndex <= endIndex <= len(slice)
1.实际赋值的数据长度为endIndex - startIndex

a := []int64{1, 2, 3, 4, 5}
b := a[3:5]
fmt.Println(a, b)
//[1 2 3 4 5] [4 5]

//注意：切片是引用，1.两个赋值的切片指向同一个内存地址,操作一个变量的值也会改变另一个变量的值。
b[0] = 11
fmt.Println(a, b)
//[11 2 3 4 5] [11 2 3]
fmt.Printf("%p  %p \n", a, b)
//0xc42001a0c0 0xc42001a0c0

//注意：copy切片，是指拷贝。1. copy数据的最大长度由接收者的长度决定。
c := make([]int64, 3)
num1 := copy(c, a)
fmt.Println(num1, c)
//3 [11 2 3]

//也可以手动指定要copy源切片的数据
d := make([]int64, 3)
num2 := copy(d, a[1:3])
fmt.Println(num2, d)
//1 [11 0 0]

```

### 线程安全
参考
> https://zhuanlan.zhihu.com/p/42006586

```
线程A， list=append(list,1) ，这时候 list={1}，那么新的list就是list={1,1}
线程B， list=append(list,1) ，这时候 list={1}，那么新的list就是list={1,1}

发现了没有，线程A和线程B是同时运行（多核并行运算），而且拿到的list变量也是完全一样的值，那么各自计算之后，更新list的值也是完全一样。
不论是线程A先写入内存，还是线程B先写入内存，肯定就有一次写入会覆盖之前一次写入，最终的结果是list={1,1}，而不是list={1,1,1}。
上面就是因为线程不安全，导致少写入了一个数据。

再看下加锁的情况下，为什么就安全了呢？
我们再来思考下：
线程A， lock, list=append(list,1), unlock ，这时候 list={1}，那么新的list就是 list={1,1}
线程B， lock/等待, list=append(list,1), unlock , 这时候 list={1,1}，那么新的list就是 list={1,1,1}
因为append的前后有一个加锁、解锁的指令，这样就避免了多线程同时并行执行 list=append(list,1) 的操作。
不存在并行运算，那么并发操作也就是安全了。
```

## new 和 make
- new(T) 返回 T 类型的指针 *T，该指针指向 T 的新分配的零值。
- make 用于引用类型 slice,map,channel初始化。make(T, args) 返回的是初始化之后的 T 类型的值。


## 调度器
一个Go程序对于操作系统来说只是一个用户层程序，对于操作系统而言，它的眼中只有thread.将goroutines按照一定算法放到不同的操作系统线程中去执行.就是调度器的工作。

### G-P-M模型

![image](http://tonybai.com/wp-content/uploads/goroutine-scheduler-model.png)

- G: 表示goroutine，存储了goroutine的执行stack信息、goroutine状态以及goroutine的任务函数等；另外G对象是可以重用的。
- P: 表示逻辑processor，P的数量决定了系统内最大可并行的G的数量（前提：系统的物理cpu核数>=P的数量）；P的最大作用还是其拥有的各种G对象队列、链表、一些cache和状态。
- M: M代表着真正的执行计算资源。在绑定有效的p后，进入schedule循环；而schedule循环的机制大致是从各种队列、p的本地队列中获取G，切换到G的执行栈上并执行G的函数，调用goexit做清理工作并回到m，如此反复。M并不保留G状态，这是G可以跨M调度的基础。

- P的个数由GOMAXPROCS指定，是固定的，因此限制最大并发数
- M的个数是不定的，由Go Runtime调整，默认最大限制为10000个

## 垃圾回收
### 标记清扫算法
标记清扫算法分为两阶段：标记阶段和清扫阶段。  
标记阶段，从root区域出发，扫描所有root区域的对象直接或间接引用到的对象，将这些对上全部加上标记。  
在回收阶段，扫描整个堆区，对所有无标记的对象进行回收。




## 问题
1. for 循环指针引用问题
```
for i := 0; i < 10; i++ {
	go func(i int) {
		fmt.Println("i: ", i)
	}(i)
}
//输出0~9，因为是赋值


for i := 0; i < 10; i++ {
	go func() {
		fmt.Println("i: ", i)
	}()
}
//大部分输出10，因为是引用，外部for循环很快，导致i指向的值变为10


m := make(map[string]*student)
stus := []student{
	{Name: "zhou", Age: 24},
	{Name: "li", Age: 23},
	{Name: "wang", Age: 22},
}
for _, stu := range stus {
	m[stu.Name] = &stu
}
for k, v := range m {
	fmt.Printf("key=%s,value=%v \n", k, v)
}
/*key=zhou,value=&{wang 22}
key=li,value=&{wang 22}
key=wang,value=&{wang 22}

因为第一个for中的stu被不断的赋值，最终只会有最后一个不会被覆盖。指针指向的内容就只会是最后一个。
*/
```

2.接口实现（值和引用两种）

```
type People interface {
	Speak(string) string
}
type Stduent struct{}
//值类型实现接口
func (stu Stduent) Speak(think string) (talk string) {
	if think == "bitch" {
		talk = "You are a good boy"
	} else {
		talk = "hi"
	}
	return
}

//引用类型实现接口
type Teach struct{}
func (t *Teach) Speak(think string) (talk string) {
	if think == "bitch" {
		talk = "You are a good boy"
	} else {
		talk = "hi"
	}
	return
}

func main() {
	var peo People
	//可以
	peo = Stduent{}
	peo = &Stduent{}

	peo = &Teach{}
	//不可以。引用类型实现接口，不能给接口类型附上值类型
	peo = Teach{}
}
```
3.接口 nil
```
var a interface{}
a == nil  //true

type People interface {
	Speak(string) string
}
var a People
a == nil //true

var stu Student
a = stu	
a == nil //false


var buf *bytes.Buffer
buf == nil //true

buf = new(bytes.Buffer)
buf == nil //false

```
这就牵扯到一个概念了，是关于接口值的。概念上讲一个接口的值分为两部分：一部分是类型，一部分是类型对应的值，他们分别叫：动态类型和动态值。类型系统是针对编译型语言的，类型是编译期的概念，因此类型不是一个值。


4.修改字符串。
重新赋值，原来的不能修改
```
func main() {
	a := "abcde"
	ab := []byte(a)
	ab[0] = 'x'
	for _, v := range ab {
		fmt.Println(string(v))
	}
}
x b c d e
```


# mysql

## 存储引擎

### InnoDB vs MyISAM
 mysql 5.5及之后版本默认存储引擎，和myisam不同的是，innodb是一种事务型存储引擎。也就是说，innodb是支持事务的acid特性的。
- 支持事务 
- 支持外键。
- 支持行级锁。

MyISAM是MySQL5.5版之前的默认数据库引擎，不支持事务处理。
#### 事务支持
- MyISAM：强调的是性能，每次查询具有原子性,其执行数度比InnoDB类型更快，但是不提供事务支持。
- InnoDB：提供事务支持事务，外部键等高级数据库功能。 具有事务(commit)、回滚(rollback)和崩溃修复能力(crash recovery capabilities)的事务安全(transaction-safe (ACID compliant))型表。

#### 表锁差异
- MyISAM：只支持表级锁，用户在操作myisam表时，select，update，delete，insert语句都会给表自动加锁，如果加锁以后的表满足insert并发的情况下，可以在表的尾部插入新的数据。
- InnoDB：支持事务和行级锁，是innodb的最大特色。行锁大幅度提高了多用户并发操作的新能。但是InnoDB的行锁，==只有通过索引条件检索数据才使用行级锁==，否则都会锁全表的。

- 表级锁：开销小，加锁快；不会出现死锁；锁定粒度大，发生锁冲突的概率最高，并发度最低。
- 行级锁：开销大，加锁慢；会出现死锁；锁定粒度最小，发生锁冲突的概率最低，并发度也最高。

#### 全文索引
MyISAM：支持 FULLTEXT类型的全文索引
InnoDB：不支持FULLTEXT类型的全文索引，


## 锁
锁是数据库系统区别于文件系统的重要特性锁的主要作用是管理共享资源的并发访问

### 乐观锁 vs 悲观锁

#### 乐观锁
用数据版本（Version）记录机制实现，这是乐观锁最常用的一种实现方式，一般是通过为数据库表增加一个数字类型的 “version” 字段来实现，数据每更新一次，对此version值加1。
```
update TABLE set value=2,version=version+1 where id=#{id} and version=#{version}
```

#### 悲观锁
在操作数据时，认为此操作会出现数据冲突，所以在进行每次操作时都要通过获取锁才能进行对相同数据的操作.

==共享锁和排它锁是悲观锁的不同的实现，它俩都属于悲观锁的范畴。==

##### 共享锁（读锁）
读取操作创建的锁，其他用户可以并发读取数据，但任何事务都不能对数据进行修改（获取数据上的排他锁），直到已释放所有共享锁。当如果事务对读锁进行修改操作，很可能会造成死锁。

```
窗口1：
begin;/begin work;/start transaction;  (三者选一就可以)
#(lock in share mode 共享锁)
SELECT * from TABLE where id = 1  lock in share mode;

窗口2：
update TABLE set name="www.souyunku.com" where id =1;
此时，操作界面进入了卡顿状态，过了很久超时，提示错误信息。
[SQL]update test_one set name="www.souyunku.com" where id =1;
[Err] 1205 - Lock wait timeout exceeded; try restarting transaction

如果在超时前，第一个窗口执行commit，此更新语句就会成功。
```

##### 独占锁（写锁）
gg'g写锁是独占的，是排它的，会阻塞其他的写锁和读锁。

```
排他锁使用方式：在需要执行的语句后面加上for update就可以了.当前写操作没有完成前，它会阻断其他写锁和读锁。
set autocommit=0;
# 设置完autocommit后，我们就可以执行我们的正常业务了。具体如下：
# 1. 开始事务
begin;/begin work;/start transaction; (三者选一就可以)
# 2. 查询表信息（for update加锁）
select status from TABLE where id=1 for update;
# 3. 插入一条数据
insert into TABLE (id,value) values (2,2);
# 4. 修改数据为
update TABLE set value=2 where id=1;
# 5. 提交事务
commit;/commit work
```

### 锁的颗粒度
#### 表级锁
mysql中最基本的表策略，开销最小的策略，并发性低。表级锁通常是在mysql服务器层实现的，所以虽然innodb实现了行级锁，但是在一些时候，mysql数据服务层还是会对innodb表加上表级锁。

#### 行级锁
可以最大程度的支持并发处理，同时锁的开销比表级锁要大。目前innodb和其他的存储引擎中实现了行级锁，行级锁只在存储引擎中进行实现，而mysql服务层并没有实现。 

**注意**：==行级锁都是基于索引的，如果一条SQL语句用不到索引是不会使用行级锁的，会使用表级锁。==
- 行锁的劣势：开销大；加锁慢；会出现死锁
- 行锁的优势：锁的粒度小，发生锁冲突的概率低；处理并发的能力强
- 加锁的方式：自动加锁。对于UPDATE、DELETE和INSERT语句，InnoDB会自动给涉及数据集加排他锁.

#### 间隙锁
键值在条件范围内但并不存在的记录，叫做“间隙（GAP)”
```
举例来说，假如emp表中只有101条记录，其empid的值分别是 1,2,...,100,101，下面的SQL：

Select * from  emp where empid > 100 for update;

InnoDB不仅会对符合条件的empid值为101的记录加锁，也会对empid大于101（这些记录并不存在）的“间隙”加锁。
```
InnoDB使用间隙锁的目的，一方面是为了防止幻读，以满足相关隔离级别的要求

#### 什么场景下用表锁
- 全表更新。事务需要更新大部分或全部数据，且表又比较大。若使用行锁，会导致事务执行效率低，从而可能造成其他事务长时间锁等待和更多的锁冲突。
- 多表查询。事务涉及多个表，比较复杂的关联查询，很可能引起死锁，造成大量事务回滚。这种情况若能一次性锁定事务涉及的表，从而可以避免死锁、减少数据库因事务回滚带来的开销。

### 阻塞 vs 死锁
1. 阻塞：在有些时刻，一个事务中的锁需要等待另一事务中的锁释放它所占用的资源，这就形成了阻塞。

2. 死锁：死锁是指两个或两个以上的事务，在执行过程中相互占用了对方等待的资源 .

下列方法有助于最大限度地降低死锁：
- 按同一顺序访问对象。
- 避免事务中的用户交互。
- 保持事务简短并在一个批处理中。

解除正在死锁的状态方法：
```
查询是否锁表
show OPEN TABLES where In_use > 0;
查询进程（如果您有SUPER权限，您可以看到所有线程。否则，您只能看到您自己的线程）
show processlist
杀死进程id（就是上面命令的id列）
kill id
```

```
查看当前的事务
SELECT * FROM INFORMATION_SCHEMA.INNODB_TRX;
查看当前锁定的事务
SELECT * FROM INFORMATION_SCHEMA.INNODB_LOCKS;
查看当前等锁的事务
SELECT * FROM INFORMATION_SCHEMA.INNODB_LOCK_WAITS;
杀死进程
kill 进程ID
```



## 索引
索引是对数据库表中一或多个列的值进行排序的结构，是帮助MySQL高效获取数据的数据结构


### 索引类型

#### 数据结构角度
##### B+Tree
> https://zhuanlan.zhihu.com/p/54102723

最常见的索引类型，基于B+Tree数据结构。B+Tree的基本思想是，所有值（被索引的列）都是排过序的，每个叶节点到跟节点距离相等。所以B+Tree适合用来查找某一范围内的数据，而且可以直接支持数据排序（ORDER BY）

![image](https://i.loli.net/2019/03/19/5c906b074d950.png)

**B+Tree**
1. 每个元素不保存数据，只用来索引，所有数据都保存在叶子节点。
2. 所有的叶子结点中包含了全部元素的信息，及指向含这些元素记录的指针，且叶子结点本身依关键字的大小自小而大顺序链接。
3. 所有的中间节点元素都同时存在于子节点，在子节点元素中是最大（或最小）元素。

**相比B-Tree 有三个优点**
1. 单一节点存储更多的元素，使得查询的IO次数更少。
2. 所有查询都要查找到叶子节点，查询性能稳定。
3. 所有叶子节点形成有序链表，便于范围查询。

##### Hash索引
基于hash表。所以这种索引只支持精确查找，不支持范围查找，不支持排序。这意味着范围查找或ORDER BY都要依赖server层的额外工作。

#### 从逻辑角度
##### 主键索引  
特殊的唯一索引，不允许有空值。主键是一种唯一性索引，==每个表只能有一个主键==，在单表查询中，PRIMARY主键索引与UNIQUE唯一索引的检索效率并没有多大的区别，但在关联查询中，PRIMARY主键索引的检索速度要高于UNIQUE唯一索引。

##### 普通索引
最基本的索引，没有任何约束限制。

##### 唯一索引
和普通索引类似，但是具有唯一性约束。

##### 复合索引
复合索引指多个字段上创建的索引，使用复合索引时遵循最左前缀集合.
分别三次建立了INDEX 普通索引,会分别检索三条索引.如果用联合索引只会一次检索三条索引。

##### 全文索引
全文索引只可以在VARCHAR或者TEXT类型的列上创建。

 **注意**：==首先检索辅助索引获得数据记录主键，然后用主键到主索引中检索获得数据记录==

### 使用原则
1. 最适合创建索引的列是出现在WHERE或ON子句中的列，或连接子句中的列而不是出现在SELECT关键字后的列。

2. 对于字符串进行索引，应该制定一个前缀长度，可以节省大量的索引空间。

3. 避免创建过多的索引，索引会额外占用磁盘空间，降低写操作效率。

4. 联合索引最左前缀匹配原则  

5. =和in可以乱序  
比如a = 1 and b = 2 and c = 3 建立(a,b,c)索引可以任意顺序，mysql的查询优化器会帮你优化成索引可以识别的形式。

6. 尽量选择区分度高的列作为索引。值重复少

6. 索引列不能参与计算  
比如from_unixtime(create_time) = ’2014-05-29’就不能使用到索引

7. LIKE查询，%不能在前

8. 如果关键词or前面的条件中的列有索引，后面的没有，所有列的索引都不会被用到。

9. 列类型是字符串，查询时一定要给值加引号，否则索引失效。


### 聚簇索引和非聚簇索引
聚簇索引并不是一种单独的索引类型，而是一种数据存储方式。

1. MyISAM的是非聚簇索引.主索引和辅助索引没啥区别，只是主索引中的key一定得是唯一的.主键索引B+树的节点存储了主键，辅助键索引B+树存储了辅助键。表数据存储在独立的地方.由于索引树是独立的，==通过辅助键检索无需访问主键的索引树==。
2. InnoDB使用的是聚簇索引.
将主键组织到一棵B+树中，而行数据就储存在叶子节点上，若使用"where id =14"这样的条件查找主键，则按照B+树的检索算法即可查找到对应的叶节点，之后获得行数据。   
若对Name列进行条件搜索，则需要两个步骤：第一步在辅助索引B+树中检索Name，到达其叶子节点获取对应的主键。第二步使用主键在主索引B+树种再执行一次B+树检索操作，最终到达叶子节点即可获取整行数据。




### 问题
- 创建MySQL联合索引应该注意什么？
```
需遵循前缀原则
```

- 列值为NULL时，查询是否会用到索引？
```
在MySQL里NULL值的列也是走索引的.当然，如果计划对列进行索引，就要尽量避免把它设置为可空，MySQL难以优化引用了可空列的查询,它会使索引、索引统计和值更加复杂。
```

- 以下语句是否会应用索引：SELECT FROM users WHERE YEAR(adddate) < 2007;
```
不会，因为只要列涉及到运算，MySQL就不会使用索引。
```


### 优化慢查询
```
select
   count(*) 
from
   task 
where
   status=2 
   and operator_id=20839 
   and operate_time>1371169729 
   and operate_time<1371174603 
   and type=2;
```

根据最左匹配原则，最开始的sql语句的索引应该是status、operator_id、type、operate_time的联合索引；
那么索引建立成(status,type,operator_id,operate_time)就是非常正确的
```
where
   status=2 
   and operator_id=20839 
   and type=2;
   and operate_time>1371169729 
   and operate_time<1371174603 
```

#### explain 详解
```
explain SELECT * from info where uid = (
	SELECT uid from user where uid=1
)
```

id | select_type | table | type| possible_keys | key | key_len	|ref	|rows |	Extra
---|---|---|---|---|---|---|---|---|---
1|	PRIMARY	|info|	ALL	|	|	|	| |	2|	Using where
2|	SUBQUERY|	user|	const|	PRIMARY	|PRIMARY|	4|	const	|1|	Using index

##### id
-  如果是子查询，id的序号会递增，id值越大优先级越高，越先被执行
- id如果相同，可以认为是一组，从上往下顺序执行；在所有组中，id值越大，优先级越高，越先执行

##### select_type
查询中每个select子句的类型
1. SIMPLE(简单SELECT,不使用UNION或子查询等)
2. PRIMARY(查询中若包含任何复杂的子部分,最外层的select被标记为PRIMARY)
3. UNION(UNION中的第二个或后面的SELECT语句)
4.  DEPENDENT UNION(UNION中的第二个或后面的SELECT语句，取决于外面的查询)
5. UNION RESULT(UNION的结果)
6. SUBQUERY(子查询中的第一个SELECT)
7. DEPENDENT SUBQUERY(子查询中的第一个SELECT，取决于外面的查询)
8. DERIVED(派生表的SELECT, FROM子句的子查询)
9. UNCACHEABLE SUBQUERY(一个子查询的结果不能被缓存，必须重新评估外链接的第一行)

##### table
显示这一行的数据是关于哪张表的.有时不是真实的表名字,看到的是derivedx(x是个数字,我的理解是第几步执行的结果)

##### type
表示MySQL在表中找到所需行的方式，又称“访问类型”。  
**常用的类型有： ALL, index,  range, ref, eq_ref, const, system, NULL（从左到右，性能从差到好）**
 
- ALL：Full Table Scan， MySQL将遍历全表以找到匹配的行

- index: Full Index Scan，index与ALL区别为index类型只遍历索引树

- range:只检索给定范围的行，使用一个索引来选择行

- ref: 表示上述表的连接匹配条件，即哪些列或常量被用于查找索引列上的值

- eq_ref: 类似ref，区别就在使用的索引是唯一索引，对于每个索引键值，表中只有一条记录匹配，简单来说，就是多表连接中使用primary key或者 unique key作为关联条件

- const、system: 当MySQL对查询某部分进行优化，并转换为一个常量时，使用这些类型访问。如将主键置于where列表中，MySQL就能将该查询转换为一个常量,system是const类型的特例，当查询的表只有一行的情况下，使用system

- NULL: MySQL在优化过程中分解语句，执行时甚至不用访问表或索引，例如从一个索引列里选取最小值可以通过单独索引查找完成。

##### possible_keys
指出MySQL能使用哪个索引在表中找到记录，查询涉及到的字段上若存在索引，则该索引将被列出，但不一定被查询使用

##### Key
key列显示MySQL实际决定使用的键（索引）.
如果没有选择索引，键是NULL.         要想强制MySQL使用或忽视possible_keys列中的索引，在查询中使用FORCE INDEX、USE INDEX或者IGNORE INDEX。

##### key_len
表示索引中使用的字节数，可通过该列计算查询中使用的索引的长度

##### ref
表示上述表的连接匹配条件，即哪些列或常量被用于查找索引列上的值

##### rows
 表示MySQL根据表统计信息及索引选用情况，估算的找到所需的记录所需要读取的行数

##### Extra
该列包含MySQL解决查询的详细信息,有以下几种情况：
- Using where:列数据是从仅仅使用了索引中的信息而没有读取实际的行动的表返回的，这发生在对表的全部的请求列都是同一个索引的部分的时候，表示mysql服务器将在存储引擎检索行后再进行过滤

- Using temporary：表示MySQL需要使用临时表来存储结果集，常见于排序和分组查询

- Using filesort：MySQL中无法利用索引完成的排序操作称为“文件排序”

- Using join buffer：改值强调了在获取连接条件时没有使用索引，并且需要连接缓冲区来存储中间结果。如果出现了这个值，那应该注意，根据查询的具体情况可能需要添加索引来改进能。

- Impossible where：这个值强调了where语句会导致没有符合条件的行。

- Select tables optimized away：这个值意味着仅通过使用索引，优化器可能仅从聚合函数结果中返回一行

## 事务
它是一个操作序列，这些操作要么都执行，要么都不执行，它是一个不可分割的工作单位。
具有原子性，一致性,持久性，隔离性。

### 事务的隔离级别
> https://www.xttblog.com/?p=3060 https://www.cnblogs.com/yubaolee/p/10398633.html


#### 第一类丢失更新（Lost Update）
在完全未隔离事务的情况下，两个事务更新同一条数据资源，某一事务完成，另一事务异常终止，回滚造成第一个完成的更新也同时丢失 


#### 脏读
所谓脏读是指一个事务中访问到了另外一个事务未提交的数据，如下图所示：
![image](https://raw.githubusercontent.com/xmt1139057136/xttblog/master/zangdu.png)

需要说明的是脏读、不可重复读、幻读都是发生在两个事务以上的情况，只有一个事务是不存在。

#### 不可重复读
所谓不可重复读是指在一个事务内根据==同一个条件==对行记录进行多次查询，但是搜出来的==结果却不一致==。发生不可重复读的原因是在多次搜索期间查询条件覆盖的数据被其他事务修改了。看下图来方便我们理解不可重复读。
![image](https://raw.githubusercontent.com/xmt1139057136/xttblog/master/bukechongfudu.png)


#### 第二类丢失更新
不可重复读有一种特殊情况，两个事务更新同一条数据资源，==后完成的事务会造成先完成的事务更新丢失==。
![image](https://i.loli.net/2019/02/27/5c76020beb0fa.png)

#### 幻读
所谓幻读是指同一个事务内多次查询返回的==结果集不一样==（比如增加了或者减少了行记录）
![image](https://raw.githubusercontent.com/xmt1139057136/xttblog/master/huandu.png)

总结：脏读是指一个事务读取到了其他事务没有提交的数据，不可重复读是指一个事务内多次根据同一个查询条件查询出来的同一行记录的值不一样，幻读是指一个事务内多次根据同个条件查出来的记录行数不一样。为了解决事务并发带来的问题，才有了事务规范中的四个事务隔离级别，不同隔离级别对上面问题部分或者全部做了避免。

### 隔离级别
为了解决上面提及的并发问题，主流关系型数据库都会提供四种事务隔离级别。

![image](https://i.loli.net/2019/02/27/5c7602cb52f40.png)

#### 读未提交（Read Uncommitted）

在该隔离级别，所有事务都可以看到其他未提交事务的执行结果。本隔离级别是最低的隔离级别，虽然拥有超高的并发处理能力及很低的系统开销，但很少用于实际应用。因为采用这种隔离级别只能防止第一类更新丢失问题，不能解决脏读，不可重复读及幻读问题。

#### 读已提交（Read Committed）
一个事务只能看见已经提交事务所做的改变。这种隔离级别可以防止脏读问题，但会出现不可重复读及幻读问题。

#### 可重复读（Repeatable Read）
这是MySQL的默认事务隔离级别，它确保同一事务的多个实例在并发读取数据时，会看到同样的数据行。这种隔离级别可以防止除幻读外的其他问题。

#### 可串行化（Serializable）
这是最高的隔离级别，它通过强制事务排序，使之不可能相互冲突，从而解决幻读、第二类更新丢失问题。在这个级别，可以解决上面提到的所有并发问题，但可能导致大量的超时现象和锁竞争，通常数据库不会用这个隔离级别，我们需要其他的机制来解决这些问题:乐观锁和悲观锁。


### 分布式事务
分布式事务就是指事务的参与者、支持事务的服务器、资源服务器以及事务管理器分别位于不同的分布式系统的不同节点之上。

能不用分布式事务就不用，如果非得使用的话，结合自己的业务分析，看看自己的业务比较适合哪一种，是在乎强一致，还是最终一致即可。

#### 基于可靠消息服务的分布式事务
> https://juejin.im/post/5aa3c7736fb9a028bb189bca

![image](https://i.loli.net/2019/03/23/5c95a246e4081.png)

#### TCC（两阶段型、补偿型）
```
Try：尝试待执行的业务
这个过程并未执行业务，只是完成所有业务的一致性检查，并预留好执行所需的全部资源

Confirm：执行业务
这个过程真正开始执行业务，由于Try阶段已经完成了一致性检查，因此本过程直接执行，而不做任何检查。并且在执行的过程中，会使用到Try阶段预留的业务资源。

Cancel：取消执行的业务
若业务执行失败，则进入Cancel阶段，它会释放所有占用的业务资源，并回滚Confirm阶段执行的操作。
```

下面以一个转账的例子来解释下TCC实现分布式事务的过程。
```
Try
创建一条转账流水，并将流水的状态设为交易中
将用户A的账户中扣除100元（预留业务资源）
Try成功之后，便进入Confirm阶段
Try过程发生任何异常，均进入Cancel阶段

Confirm
向B用户的红包账户中增加100元
将流水的状态设为交易已完成
Confirm过程发生任何异常，均进入Cancel阶段
Confirm过程执行成功，则该事务结束

Cancel
将用户A的账户增加100元
将流水的状态设为交易失败
```

## sql的优化

## join on where

uid | name
---|---
1 | name-111
2 | name-222

uid | province | city
---|---|---
1 | anhui | hefei
3 | shanghai | yangpu

### inner join
内连接查询能将左表（表 A）和右表（表 B）中能关联起来的数据连接后返回。

![image](https://raw.githubusercontent.com/mzlogin/mzlogin.github.io/master/images/posts/database/inner-join.png)

```
SELECT user.uid,info.province,info.city from `user` INNER JOIN `info` on user.uid = info.uid

uid	province  city
1	anhui	  hefei
```

### LEFT JOIN
左连接查询会返回左表（表 A）中所有记录，不管右表（表 B）中有没有关联的数据。在右表中找到的关联数据列也会被一起返回。

![image](https://raw.githubusercontent.com/mzlogin/mzlogin.github.io/master/images/posts/database/left-join.png)

```
SELECT user.uid,user.nickname,info.province,info.city from `user` LEFT JOIN `info` on user.uid = info.uid

uid	province  city
1	anhui	  hefei
2   
```

### RIGHT JOIN
右连接查询会返回右表（表 B）中所有记录，不管左表（表 A）中有没有关联的数据。在左表中找到的关联数据列也会被一起返回。

![image](https://raw.githubusercontent.com/mzlogin/mzlogin.github.io/master/images/posts/database/right-join.png)

```
SELECT user.uid,user.nickname,info.province,info.city from `user` RIGHT JOIN `info` on user.uid = info.uid

uid	province  city
1	anhui	  hefei
    shanghai  yangpu
```

注意：mysql不支持Full join,不过可以通过UNION 关键字来合并 LEFT JOIN 与 RIGHT JOIN来模拟FULL join.


# Redis
redis支持string,list,hash,set,zset，Bitmaps，Hyperloglogs ，地理空间（Geospatial），Pub/Sub 

使用单进程单线程的IO复用模型，官方提供的数据是可以达到100000+的QPS（每秒内查询次数）

Redis 内置了复制（Replication），LUA脚本（Lua scripting）， LRU驱动事件（LRU eviction），事务（Transactions） 和不同级别的磁盘持久化（Persistence），并通过 Redis哨兵（Sentinel）和自动分区（Cluster）提供高可用性（High Availability）。

## Redis为什么这么快
1. 完全基于内存，绝大部分请求是纯粹的内存操作，非常快速。数据存在内存中，类似于HashMap，HashMap的优势就是查找和操作的时间复杂度都是O(1)；

2. 数据结构简单，对数据操作也简单，Redis中的数据结构是专门进行设计的；

3. 采用单线程，避免了不必要的上下文切换和竞争条件，也不存在多进程或者多线程导致的切换而消耗 CPU，不用去考虑各种锁的问题，不存在加锁释放锁操作，没有因为可能出现死锁而导致的性能消耗；

4. ==使用多路I/O复用模型，非阻塞IO；==  
这里“多路”指的是多个网络连接，“复用”指的是复用同一个线程。多路I/O复用模型是利用 select、poll、epoll 可以同时监察多个流的 I/O 事件的能力，在空闲的时候，会把当前线程阻塞掉，当有一个或多个流有 I/O 事件时，就从阻塞态中唤醒。

**==警告1==**：这里我们一直在强调的单线程，只是在处理我们的网络请求的时候只有一个线程来处理，一个正式的Redis Server运行的时候肯定是不止一个线程的，


==**注意点**==
耗时的命令会导致并发的下降，不只是读并发，写并发也会下降。而单一线程也只能用到一个CPU核心，所以可以在同一个多核的服务器中，可以启动多个实例，组成master-master或者master-slave的形式，耗时的读命令可以完全在slave进行。

## 持久化
有两种持久化的方式：快照（RDB文件）和追加式文件（AOF文件）：
- RDB持久化方式会在一个特定的间隔保存那个时间点的一个数据快照。
- AOF持久化方式则会记录每一个服务器收到的写操作。在服务启动时，这些记录的操作会逐条执行从而重建出原来的数据。写操作命令记录的格式跟Redis协议一致，以追加的方式进行保存。
- 两种方式的持久化是可以同时存在的，但是当Redis重启时，AOF文件会被优先用于重建数据。

### 快照 RDB
Redis调用fork()，产生一个子进程,子进程把数据写到一个临时的RDB文件,当子进程写完新的RDB文件后，把旧的RDB文件替换掉。  
Redis会把快照文件存储为当前目录下一个名为dump.rdb的文件

优点：
- RDB文件是一个很简洁的单文件，它保存了某个时间点的Redis数据，很适合用于做备份
- RDB的性能很好，需要进行持久化时，主进程会fork一个子进程出来，然后把持久化的工作交给子进程，自己不会有相关的I/O操作。
- 比起AOF，在数据量比较大的情况下，RDB的启动速度更快。

缺点：
- 容易造成数据的丢失，假设每5分钟保存一次快照，如果Redis因为某些原因不能正常工作，那么从上次产生快照到Redis出现问题这段时间的数据就会丢失了。

### AOF
每当Redis接受到会修改数据集的命令时，就会把命令追加到AOF文件里，当你重启Redis时，AOF里的命令会被重新执行一次，重建数据。

优点：
- 比RDB可靠。你可以制定不同的fsync策略：不进行fsync、每秒fsync一次和每次查询进行fsync。默认是每秒fsync一次。这意味着你最多丢失一秒钟的数据。
- AOF日志文件是一个纯追加的文件。就算是遇到突然停电的情况，也不会出现日志的定位或者损坏问题。
- 当AOF文件太大时，Redis会自动在后台进行重写。
- AOF把操作命令以简单易懂的格式一条接一条的保存在文件里，很容易导出来用于恢复数据。例如我们不小心用FLUSHALL命令把所有数据刷掉了，只要文件没有被重写，我们可以把服务停掉，把最后那条命令删掉，然后重启服务，这样就能把被刷掉的数据恢复回来。

缺点：
- 在相同的数据集下，AOF文件的大小一般会比RDB文件大。

## 同步机制
　和MySQL主从复制的原因一样，Redis虽然读取写入的速度都特别快，但是也会产生读压力特别大的情况。为了分担读压力，Redis支持主从复制，Redis的主从结构可以采用一主多从或者从从结构，
　
主从刚刚连接的时候，进行全量同步；全同步结束后，进行增量同步。

### 全量同步
Redis全量复制一般发生在Slave初始化阶段，这时Slave需要将Master上的所有数据都复制一份。具体步骤如下： 
1. 从服务器连接主服务器，发送SYNC命令； 
2. 主服务器接收到SYNC命名后，开始执行BGSAVE命令生成RDB文件并使用缓冲区记录此后执行的所有写命令； 
3. 主服务器BGSAVE执行完后，向所有从服务器发送快照文件，并在发送期间继续记录被执行的写命令； 
4. 从服务器收到快照文件后丢弃所有旧数据，载入收到的快照； 
5. 主服务器快照发送完毕后开始向从服务器发送缓冲区中的写命令； 
6. 从服务器完成对快照的载入，开始接收命令请求，并执行来自主服务器缓冲区的写命令； 


## 集群 
1. 集群需要最少三个节点
2. 将数据自动切分（split）到多个节点的能力。  
  集群使用公式 CRC16(key) % 16384 来计算键 key 属于哪个槽

### 分片 Redis Cluster
集群中的每个节点负责处理一部分哈希槽。 举个例子， 一个集群可以有三个哈希槽， 其中：
- 节点 A 负责处理 0 号至 5500 号哈希槽。
- 节点 B 负责处理 5501 号至 11000 号哈希槽。
- 节点 C 负责处理 11001 号至 16384 号哈希槽。  

如果用户将新节点 D 添加到集群中， 那么集群只需要将节点 A 、B 、 C 中的某些槽移动到节点 D 就可以了。

为了使得集群在一部分节点下线或者无法与集群的大多数（majority）节点进行通讯的情况下， 仍然可以正常运作， Redis 集群对节点使用了==主从复制功能==

### 哨兵 Sentinel
针对从节点升级为主节点，是使用哨兵（sentinel）来进行操作的。
1. 监控主数据库和从数据库是否正常运行。 
2. 主数据库出现故障时自动将从数据库转换为主数据库。

哨兵是一个单独的节点来监听主节点  
配置文件
```
 sentinel.conf 
 sentinel monitor mymaster 192.168.0.167 6379 1 
 
 1.mymaster表示要监控的主数据库的名字，可以自己定义一个.
 2.配置哨兵监控一个系统时，只需要配置其监控主数据库即可，哨兵会自动发现所有复制该主数据库的从数据库
```

![image](https://i.loli.net/2019/03/17/5c8e09cec6c97.png)


## 数据淘汰机制

1. 最大缓存
```
在 redis 中，允许用户设置最大使用内存大小server.maxmemory，默认为0，没有指定最大缓存，如果有新的数据添加，超过最大内存，则会使redis崩溃，所以一定要设置。
redis 内存数据集大小上升到一定大小的时候，就会实行数据淘汰策略。
```

- voltile-lru：从已设置过期时间的数据集（server.db[i].expires）中挑选最近最少使用的数据淘汰
- volatile-ttl：从已设置过期时间的数据集（server.db[i].expires）中挑选将要过期的数据淘汰
- volatile-random：从已设置过期时间的数据集（server.db[i].expires）中任意选择数据淘汰
- allkeys-lru：从数据集（server.db[i].dict）中挑选最近最少使用的数据淘汰
- allkeys-random：从数据集（server.db[i].dict）中任意选择数据淘汰
- no-enviction（驱逐）：禁止驱逐数据




## 题目
1. 分布式锁
```
1. 它是什么回事？
先拿setnx来争抢锁，抢到之后，再用expire给锁加一个过期时间防止锁忘记了释放。

2.如果在setnx之后执行expire之前进程意外crash或者要重启维护了，那会怎么样？
把两个命令封装成一个事务执行。
```

2.假如Redis里面有1亿个key，其中有10w个key是以某个固定的已知的前缀开头的，如果将它们全部找出来？
```
使用keys指令可以扫出指定模式的key列表.
redis的单线程的,keys指令会导致线程阻塞一段时间，线上服务会停顿，直到指令执行完毕，服务才能恢复。

可以使用scan指令，scan指令可以无阻塞的提取出指定模式的key列表，但是会有一定的重复概率，在客户端做一次去重就可以了，但是整体所花费的时间会比直接用keys指令长。

scan:
命令用于迭代当前数据库中的数据库键。
1.scan命令的时间复杂度虽然也是O(N)，但它是分次进行的，不会阻塞线程。
2.scan命令提供了limit参数，可以控制每次返回结果的最大条数。
```

3.使用过Redis做异步队列么，你是怎么用的？
```
1.一般使用list结构作为队列，rpush生产消息，lpop消费消息。当lpop没有消息的时候，要适当sleep一会再重试。
2.list还有个指令叫blpop，在没有消息的时候，它会阻塞住直到消息到来。

能不能生产一次消费多次呢？
使用pub/sub主题订阅者模式，可以实现1:N的消息队列。

缺点？
在消费者下线的情况下，生产的消息会丢失，得使用专业的消息队列如rabbitmq等。

redis如何实现延时队列?
zset,拿时间戳作为score，消息内容作为key调用zadd来生产消息，消费者用zrangebyscore指令获取N秒之前的数据轮询进行处理。
```
4.Pipeline有什么好处，为什么要用pipeline？
```
可以将多次IO往返的时间缩减为一次，前提是pipeline执行的指令之间没有因果相关性。
```

5.Redis的同步机制了解么？
```
Redis可以使用主从同步，从从同步。第一次同步时，主节点做一次bgsave把数据写到rdb文件，并同时将后续修改操作记录到内存buffer，待完成后将rdb文件全量同步到复制节点，复制节点接受完成后将rdb镜像加载到内存。加载完成后，再通知主节点将期间修改的操作记录同步到复制节点进行重放就完成了同步过程。
```

6.是否使用过Redis集群，集群的原理是什么？
```
1.Redis Sentinal着眼于高可用，在master宕机时会自动将slave提升为master，继续提供服务。
2.Redis Cluster着眼于扩展性，在单个redis内存不足时，使用Cluster进行分片存储。
```




# 算法

> https://www.cnblogs.com/onepixel/p/7674659.html

## 冒泡排序 O(N2)

```
func maoPai()  {
	f := false
	a := []int{5, 2, 6, 3}
	for i := 0; i < len(a)-1; i++ {
		for j := 0; j < len(a)-1; j++ {
			if a[j] > a[j+1] {
				a[j], a[j+1] = a[j+1], a[j]
				f = true
			}
		}

		fmt.Println(a)
		//整个内循环都没有发生位置互换，表示都满足排序了
		if !f {
			break
		}
	}
}

[2 5 3 6]
[2 3 5 6]
[2 3 5 6]
```

## 选择排序
```
func selectPai() {
	arr := []int{5, 2, 6, 3}
	//第一轮循环找到数组中最小的值，放到左边
	//第二轮循环找到数组中最次小的值，放到左边
	//。。。。。。
	minIdx := 0
	for i := 0; i < len(arr); i++ {
		minIdx = i
		for j := i + 1; j < len(arr); j++ {
			if arr[j] < arr[minIdx] {
				minIdx = j
			}
		}
		if minIdx > i {
			arr[i], arr[minIdx] = arr[minIdx], arr[i]
		}
	}

	fmt.Println(arr)
}

[2 5 6 3]
[2 3 6 5]
[2 3 5 6]
[2 3 5 6]
```

## 插入排序
```
func insertPai() {
	arr := []int{5, 2, 6, 3}
	//从第二个值开始，向前（左）遍历，遇到比当前大的，对调位置，再减一继续遍历前面的。
	//为什么是对调下当前两个位置？因为前面都已经排序了，从小到大
	for i := 1; i < len(arr); i++ {
		//为什么把当前i的值复制一份，因为对调位置的话，arr[i]的值就变了。所以下面的比较不能用arr[i]
		current := arr[i]
		preIdx := i - 1

		for preIdx >= 0 && arr[preIdx] > current {
			arr[preIdx], arr[preIdx+1] = arr[preIdx+1], arr[preIdx]
			preIdx--
		}
		fmt.Println(arr)
	}
}

[2 5 6 3]
[2 5 6 3]
[2 3 5 6]
```

## 快速排序

> https://blog.csdn.net/MoreWindows/article/details/6684558

```
package main
import "fmt"

func main() {
	a := []int{5, 1, 9, 0, 2, 7}
	quick(a, 0, len(a)-1)
}

func quick(a []int, l, r int) {
	if l < r {
		i := keng(a, l, r)
		fmt.Println(l, r, a, i)

		//再把i位置左边的所有数排序一次
		quick(a, l, i-1)
		//再把i位置右边的所有数排序一次
		quick(a, i+1, r)
	}
}

//分块，随机选择一个数x，这里选择最左的i=0  x=a[0]。相当于i的坑位是空的了
func keng(a []int, l, r int) int {
	i := l
	j := r
	x := a[i]

	for i < j {
		//先从最后一个开始遍历，遇到比x大的，减一，再比较，直到遇到比x小的, 把j位置上的值放到i空位上，j位置为空，结束从后向前的遍历
		for i < j {
			if a[j] >= x {
				j--
			} else {
				a[i], a[j] = a[j], a[i]
				i++
				break
			}
		}

		//再从i+1的位置从前向后遍历比较，遇到比x小的，加一，再比较，直到遇到比x大的，把当前i的值放到空位j上，结束从前向后遍历。再开始从后向前
		for i < j {
			if a[i] < x {
				i++
			} else {
				a[i], a[j] = a[j], a[i]
				j--
				break
			}
		}
	}
	//最后i==j,结束此轮，把x放到空位上，此时x左边的数都比x小，右边的都比x大
	a[i] = x
	return i
}
```

## 计数排序
适用于==一定范围的整数排序==。数字作为数组的key，值为数字出现的次数
```
func jishu() {
	a := []int{3, 1, 2, 6, 2, 9}
	b := [10]int{}
	for _, v := range a {
		if b[v] > 0 {
			b[v]++
		} else {
			b[v] = 1
		}
	}

	c := make([]int, 0)
	for k, v := range b {
		for i := 0; i < v; i++ {
			c = append(c, k)
		}
	}
	fmt.Println(c)
}

[1 2 2 3 6 9]
```

## 动态规划
### 上台阶问题
10级台阶，一次可以上1级或2级，总共有多少种上法？  
分析

级数 | 上法
---|---
1 | (1)
2 | (1,1)(2)
3 | (1,1,1)(1,2)(2,1)
4 | (1,1,1,1)(1,1,2)(1,2,1)(2,1,1)(2,2)

可以得到第n级为：f(n) = f(n-1) + f(n-2)

```
func stage(n int) (i int) {
	if n == 1 {
		i = 1
	} else if n == 2 {
		i = 2
	} else if n > 2 {
		i = stage(n-1) + stage(n-2)
	}
	return
}
```


## 二分查找
```
func main() {
	a := []int{1, 2, 3, 4, 5}
	s := 41
	i := zheBanSearch2(a, s, 0, len(a)-1)
	fmt.Println(i)
}
//循环实现
func zheBanSearch2(a []int, s, l, r int) (i int) {
	i = -1
	for l < r {
		m := l + (r-l)/2
		if a[m] == s {
			i = m
			break
		} else if a[m] > s {
			r = m - 1
		} else if a[m] < s {
			l = m + 1
		}
	}
	return
}
//递归实现
func zheBanSearch(a []int, s, l, r int) (i int) {
	m := l + (r-l)/2
	if a[m] == s {
		i = m
	} else if a[m] > s {
		i = zheBanSearch(a, s, l, m-1)
	} else if a[m] < s {
		i = zheBanSearch(a, s, m+1, r)
	}
	return
}
```

## hash查找
Hash是一种典型以空间换时间的算法。将键作为索引，值即为其对应的值，这样就可以快速访问任意键的值。


## 加密算法
> https://juejin.im/post/5b48b0d7e51d4519962ea383

1. 对称加密 ： DES、3DES、AES 等
2. 非对称算法 ： RSA、DSA 等
3. 散列算法 ：SHA-1、MD5 等。



# linux
> http://www.runoob.com/linux/linux-command-manual.html

## 常用命令

### awk
文本内容:
```
1 2 3 4
a,b,c,d
```
- F:指定输入文件折分隔符
```
1.数据每行第一个和第四个字符
awk '{print $1,$4}' test.txt

1 4
a,b,c,d

2.按逗号分隔，输出第一个和第四个字符
awk -F , '{print $1,$4}' test.txt

1 2 3 4
a d

3.使用多个分隔符，输出第一个和第四个
awk -F '[, ]' '{print $1,$4}' test.txt

1 4
a d
```
- v 
赋值一个用户定义变量。
```
1. 每行第一个字符加100
awk -F '[, ]' -v a=100 '{print $1+a,$4}' test.txt

101 4
100 d
```

- 运算符
```
1. 过滤第一列等于1的行
awk -F '[, ]' '$1==1 {print $1,$2,$3,$4}' test.txt

1 2 3 4
```

### grep
grep命令用于查找文件里符合条件的字符串。
```
1.查找当前目录下后缀为.txt并且内容有kang的文件.打印出这一行内容
grep kang *.txt

test.txt:kang123

2.以递归的方式查找符合条件的文件
grep -r update /etc/acpi 

3、反向查找。查找文件名中包含 test 的文件中不包含test 的行，此时，使用的命令为：
grep -v test *test*
```


# 网络
## 七层协议
1. 应用层  
各种应用程序协议，如http，ftp，smtp

2. 表示层  
信息的语法语义以及它们的关联，如加密解密，转换翻译，压缩解压

3. 会话层  
不同机器用户之间建立和管理会话

4. 传输层  
接收上一层数据，在必要的时候把数据进行分割，并将这些数据交给网络层，且保证这些数据段有效到达对端。tcp/udp协议。

5. 网络层  
控制子网的运行，如逻辑编址，分组传输，路由选择。

6. 数据链路层  
物理寻址，同时将原始比特流转变为逻辑传输线路。

7. 物理层  
机械，电子，定时接口通信信道上的原始比特流传输


### 四层协议
1. 应用层  
包含了应用层，表示层，会话层
2. 传输层
3. 网络层
4. 物理层  
包含了数据链路层，物理层

## TCP UDP的区别
- TCP面向连接，UDP面向非连接即发送数据前不需要建立链接
- TCP提供可靠的服务（数据传输），UDP无法保证
- TCP面向字节流，UDP面向报文
- TCP数据传输慢，UDP数据传输快

## TCP的三次握手
![image](https://i.loli.net/2019/03/12/5c8726cc3aa33.png)

## 在浏览器中输入网址之后执行会发生什么？
- 查找域名对应的IP地址。这一步会依次查找浏览器缓存，系统缓存，路由器缓存，ISPNDS缓存，根域名服务器
- 浏览器向IP对应的web服务器发送一个HTTP请求
- 服务器响应请求，发回网页内容
- 浏览器解析网页内容


# 操作系统 

## 进程线程协程
1. 进程是具有一定功能的程序关于某个数据集合上的一次运行活动，进程是系统进行资源调度和分配的一个独立单位。
2. 线程是进程的实体，是CPU调度和分派的基本单位，它是比进程更小的能独立运行的基本单位。
3. 一个进程可以有多个线程，多个线程也可以并发执行
4. 协程：协程是一种用户态的轻量级线程，协程的调度完全由用户控制。

## 什么是死锁？死锁产生的条件？
在两个或者多个并发进程中，如果每个进程持有某种资源而又等待其它进程释放它或它们现在保持着的资源，在未改变这种状态之前都不能向前推进，称这一组进程产生了死锁。通俗的讲就是两个或多个进程无限期的阻塞、相互等待的一种状态。

死锁产生的四个条件（有一个条件不成立，则不会产生死锁）
- 互斥条件：一个资源一次只能被一个进程使用
- 请求与保持条件：一个进程因请求资源而阻塞时，对已获得资源保持不放
- 不剥夺条件：进程获得的资源，在未完全使用完之前，不能强行剥夺
- 循环等待条件：若干进程之间形成一种头尾相接的环形等待资源关系 


# 其他
- hash表

# 原因
- 加班比较多，个人时间很少，缺少时间发展自身，比如新技能，健康，家庭等。
- 呆了两年，组织架构经常调整，经历了公司很多业务部门，缺少成就感，想换个稳定的更好的平台来施展
