# （一）：认知Handler

https://juejin.cn/post/6887918066043191304

## 什么是Handler？

Handler机制是Android中基于单线消息队列模式的一套线程消息机制

## 两个关键问题

+ 不能在非UI创建线程去操作UI
+ 不能在主线程执行耗时任务

## 为什么要有Handler？

+ 切换代码执行的线程
  
  + rxjava rxbus 协程 ansyctask都可以切线程

+ 按顺序规则地处理消息，避免并发
  
  + 单线消息队列模型

+ 阻塞线程，避免让线程结束
  
  + 我们执行一个Java程序的时候，从main方法入口，执行完成之后，马上就退出了，但是我们android应用程序肯定是不可以的，他需要一直等待用户的操作。而Handler机制就解决了这个问题，但消息队列中没有任务的时候，他就会把线程阻塞，等到有新的任务的时候，再重新启动处理消息

+ 延迟处理消息

## 如何使用Handler

+ 创建Looper
  + **每个线程只有一个Looper**
+ 使用Looper创建Handler
+ 启动Looper
+ 使用Handler发送信息

# （二）：ThreadLocal

# （三）：内部关键类

## Message

### 循环利用Message

Message维护了一个静态链表，链表头是`sPool`,Message有一个next属性，Message本身就是链表结构。`sPoolSync`是一个object对象，仅作为解决并发访问安全设计。当我们调用obtain来获取一个新的Message的时候，首先会检查链表中是否有空闲的Message，如果没有则新建一个返回

### Message总结

同时官方建议不要直接初始化Message，而是通过Message.obtain()方法来获取一个Message循环利用。一般来说我们不需要去调用recycle进行回收，在Looper中会自动把Message进行回收

## MessageQueue

当MessageQueue中没有消息或者都在等待中，则会将线程休眠，让出cpu资源，提高cpu的利用效率。进入休眠后，如果需要继续执行代码则需要将线程唤醒。当方法暂时无法直接返回需要等待的时候，则可以将线程阻塞，即休眠，等待被唤醒继续执行逻辑

### 关键方法

出队 -- next()

+ 如果Looper已经退出了，直接返回null
+ 进入死循环，直到获取到Message或者退出
+ 循环中先判断是否需要进行阻塞，阻塞结束后，对MessageQueue进行加锁，获取Message
+ 如果MessageQueue中没有消息，则直接把线程无限阻塞等待唤醒；
+ 如果MessageQueue中有消息，则判断是否需要等待，否则则直接返回对应的message

入队 -- enqueueMessage()

+ 首先判断message的目标handler不能为空且不能正在使用中
+ 对MessageQueue进行加锁
+ 判断目标线程是否已经死亡，死亡则直接返回false
+ 初始化Message的执行时间以及标记正在执行中
+ 然后根据Message的执行时间，找到在链表中的插入位置进行插入
+ 同时判断是否需要唤醒MessageQueue。有两种情况需要唤醒：当新插入的Message在链表头时，如果messageQueue是空的或者正在等待下个任务的延迟时间执行，这个时候就需要唤醒MessageQueue

## Looper

### 概述

Looper可以说是Handler机制中的一个非常重要的核心。Looper相当于线程消息机制的引擎，驱动整个消息机制运行。Looper负责从队列中取出消息，然后交给对应的Handler去处理。如果队列中没有消息，则MessageQueue的next方法会阻塞线程，等待新的消息的到来。每个线程有且只能有一个“引擎”，也就是Looper，如果没有Looper，那么消息机制就运行不起来，而如果有多个Looper，则会违背单线操作的概念，造成并发操作

每个线程仅有一个Looper，由不同Looper分发的Message运行在不同的线程中。Looper的内部维护一个MessageQueue，当初始化Looper的时候会顺带初始化MessageQueue

Looper使用ThreadLocal来保证每个线程都有且只有一个相同的副本

### 关键方法

loop() : 循环获取消息

loop()方法就是Looper这个“引擎”的核心所在。首先获取当前线程的Looper对象，没有则抛出异常。然后进入一个死循环：不断调用MessageQueue的next方法来获取消息，然后调用message的目标handler的dispatchMessage方法来处理Message

前面我们了解过了MessageQueue，next方法是可能会进行阻塞的：当MessageQueue为空或者目前没有任何消息需要处理。所以Looper就会一直等待，阻塞在里，线程也就不会结束。当我们退出Looper的时候，next方法会返回null，那么Looper也就会跟着结束了

同时，因为Looper是运行在不同线程的逻辑，其调用的dispatchMessage方法也是运行在不同的线程，这就达到了切换线程的目的

quit/quitSafely : 退出Looper

quit是直接将Looper退出，quitSafely是将MessageQueue中的**不需要等待的消息**处理完成之后再退出

# （四）：内部关键类

## Handler

### 内存泄露问题

当我们使用继承Handler方法来使用Handler的时候，要注意使用静态内部类，而不要用非静态内部类。因为非静态内部类会持有外部类的引用，而从上面的分析我们知道Message在被入队之后他的target属性是指向了Handler，如果这个Message是一个延迟的消息，那么这一条引用链的对象就迟迟无法被释放，造成内存泄露

## HandlerThread

# （五）：再认知Handler

Handler机制使用的是多线程的思路，主线程不断等待消息，然后从别的线程发送消息让主线程执行逻辑，这也称为**事务驱动型设计**，主线程的逻辑都是通过message来驱动的

**当应用进程被创建的时候，只是创建了主线程的Looper和handler，以及其他的binder线程等。之后AMS通过Binder与应用程序通信，给主线程发送message，让程序执行创建Activity等的操作**

# （终篇）：常见问题汇总

## 为什么主线程的Looper是一个死循环，但是却不会ANR？

答： 因为当Looper处理完所有消息的时候会进入阻塞状态，当有新的Message进来的时候会打破阻塞继续执行

这其实没理解好ANR这个概念。ANR，全名Application Not Responding。当我发送一个绘制UI 的消息到主线程Handler之后，经过一定的时间没有被执行，则抛出ANR异常。Looper的死循环，是循环执行各种事务，包括UI绘制事务。Looper死循环说明线程没有死亡，如果Looper停止循环，线程则结束退出了。Looper的死循环本身就是保证UI绘制任务可以被执行的原因之一。同时UI绘制任务有同步屏障，可以更加快速地保证绘制更快执行

## Handler如何保证MessageQueue并发访问安全？

循环加锁，配合阻塞唤醒机制

我们可以发现MessageQueue其实是“生产者-消费者”模型，Handler不断地放入消息，Looper不断地取出，这就涉及到死锁问题。如果Looper拿到锁，但是队列中没有消息，就会一直等待，而Handler需要把消息放进去，锁却被Looper拿着无法入队，这就造成了死锁。Handler机制的解决方法是**循环加锁**。在MessageQueue的next方法中，我们可以看到他的等待是在锁外的，当队列中没有消息的时候，他会先释放锁，再进行等待，直到被唤醒。这样就不会造成死锁问题了

## Handler的阻塞唤醒机制是怎么回事？

## 能不能让一个Message加急被处理？/ 什么是Handler同步屏障？

如果向主线程发送了一个UI更新的操作Message，而此时消息队列中的消息非常多，那么这个Message的处理就会变得缓慢，造成界面卡顿。所以通过同步屏障，可以使得UI绘制的Message更快被执行

[关于Handler同步屏障你可能不知道的问题](https://juejin.cn/post/6940607471153053704)

## 什么是IdleHandler？

当MessageQueue为空或者目前没有需要执行的Message时会回调的接口对象

在MessageQueue中有一个List存储了IdleHandler对象，当MessageQueue没有需要被执行的Message时就会遍历回调所有的IdleHandler。所以IdleHandler主要用于在消息队列空闲的时候处理一些**轻量级**的工作