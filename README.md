# -Linux-
# 一级标题  
<br>
## 第一章 线程安全的对象生命周期管理 
### 1.构造函数的作用是构造对象，初始化，不要泄露对象的指针，调用成员函数。
### 2.一个函数如果要锁住相同类型的多个对象，为了避免死锁（多个锁，顺序不同可能出现），可以比较mutex对象的地址，始终先加锁地址较小的muex。
### 3.使用智能指针 shared_ptr 做函数参数最好用常引用 防止拷贝 延长对象生命周期
<br>
## 第二章 线程同步精要
### 1.最低限度地共享对象，减少需要同步场合。
### 2.尽量用高层同步设施，不得已使用底层同步原语时，只用非递归的互斥器和条件变量，慎用读写锁，不要用信号量。<br>
（递归锁：同一个线程可以多次获取同一个递归锁，不会产生死锁。<br>
  非递归锁：如果一个线程多次获取同一个非递归锁，则会产生死锁。Linux下pthread_mutex_t锁是默认是非递归的。）
### 3.条件变量的使用。<br>
等待端（消费者）<br>
 a.mutex lock<br>
 b.while(empty){ //没有任务<br>
     cond.wait()<br>
 }<br>
 c.if(!empty) dowork remove//再判断 完成任务 移除任务<br>
 通知端（生产者）<br>
 a.mutex lock<br>
 b.insert<br>
 c.cond.notify<br>
 ## 第三章 多线程服务器的适用场合与常用编程模型
 ### 1.进程间通信首选Sockets(TCP) 可以跨主机，具有伸缩性
