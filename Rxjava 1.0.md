# Rxjava 1.0

[给 Android 开发者的 RxJava 详解](https://gank.io/post/560e15be2dca930e00da1083)

+ 基本实现
  + 创建 Observer
    + onStart(): 这是 Subscriber 增加的方法。它会在 subscribe 刚开始，而事件还未发送之前被调用，可以用于做一些准备工作，例如数据的清零或重置。这是一个可选方法，默认情况下它的实现为空。需要注意的是，如果对准备工作的线程有要求（例如弹出一个显示进度的对话框，这必须在主线程执行）， onStart() 就不适用了，因为它总是在 subscribe 所发生的线程被调用，而不能指定线程。要在指定的线程来做准备工作，可以使用 doOnSubscribe() 方法
    + unsubscribe(): 这是 Subscriber 所实现的另一个接口 Subscription 的方法，用于取消订阅。在这个方法被调用后，Subscriber 将不再接收事件。一般在这个方法调用前，可以使用 isUnsubscribed() 先判断一下状态。 unsubscribe() 这个方法很重要，因为在 subscribe() 之后， Observable 会持有 Subscriber 的引用，这个引用如果不能及时被释放，将有内存泄露的风险。所以最好保持一个原则：要在不再使用的时候尽快在合适的地方（例如 onPause() onStop() 等方法中）调用 unsubscribe() 来解除引用关系，以避免内存泄露的发生
  + 创建 Observable
    + create()
    + just(T...): 将传入的参数依次发送出来
    + from(T[]) / from(Iterable<? extends T>) : 将传入的数组或 Iterable 拆分成具体对象后，依次发送出来
    + 若未发送onComplete，会造成线程无法回收
+ 线程控制 —— Scheduler 
  + subscribeOn(): 指定 subscribe() 所发生的线程，即 Observable.OnSubscribe 被激活时所处的线程。或者叫做事件产生的线程
    + 不同于 observeOn() ， subscribeOn() 的位置放在哪里都可以，但它是只能调用一次的
  +  observeOn(): 指定 Subscriber 所运行在的线程。或者叫做事件消费的线程
    + observeOn() 指定的是它之后的操作所在的线程。因此如果有多次切换线程的需求，只要在每个想要切换线程的位置调用一次 observeOn() 即可
  + doOnSubscribe()
    + 它和 Subscriber.onStart() 同样是在 subscribe() 调用后而且在事件发送前执行，但区别在于它可以指定线程。默认情况下， doOnSubscribe() 执行在 subscribe() 发生的线程；而如果在 doOnSubscribe() 之后有 subscribeOn() 的话，它将执行在离它最近的 subscribeOn() 所指定的线程

+ 变换
  + map()
  + flatMap()

[浅谈RxJava与多线程并发](http://zjutkz.net/2017/02/09/%E6%B5%85%E8%B0%88RxJava%E4%B8%8E%E5%A4%9A%E7%BA%BF%E7%A8%8B%E5%B9%B6%E5%8F%91/)

[浅谈RxJava中的线程管理](http://zjutkz.net/2017/04/26/%E6%B5%85%E8%B0%88RxJava%E4%B8%AD%E7%9A%84%E7%BA%BF%E7%A8%8B%E7%AE%A1%E7%90%86/)

[关于RxJava最友好的文章——背压（Backpressure）](https://juejin.im/post/582d413c8ac24700619cceed)

