# Rxjava 2.0

[RxJava-Android-Samples](https://github.com/kaushikgopal/RxJava-Android-Samples)

+ Background work & concurrency (using Schedulers)
+ Networking with Retrofit & RxJava 
+ Pseudo caching : retrieve data first from a cache, then a network call 
  + 测试各类merge concat，类似仓库模式？？？
+ RxBus : event bus using RxJava (using RxRelay (never terminating Subjects) and debouncedBuffer)
  - [RxRelay](https://github.com/JakeWharton/RxRelay)
  - [Implementing an event bus with RxJava](http://blog.kaush.co/2014/12/24/implementing-an-event-bus-with-rxjava-rxbus/)
  - [DebouncedBuffer used for the fancier variant of the demo](http://blog.kaush.co/2015/01/05/debouncedbuffer-with-rxjava/)
  - [share/publish/refcount](http://blog.kaush.co/2015/01/21/rxjava-tip-for-the-day-share-publish-refcount-and-all-that-jazz/)
  - 非常棒的例子和博客
+ Accumulate calls (using buffer)
  + buffer积累点击事件，再发送
+ Instant/Auto searching text listeners
  + [debounce防抖动](https://stackoverflow.com/questions/25991367/difference-between-throttling-and-debouncing-a-function)
+ Two-way data binding for TextViews (using PublishSubject)
  + PublishProcessor
  + @OnTextChanged
+ NetworkDetectorFragment
  - distinctUntilChanged
+ Simple timing demos (using timer, interval and delay)
+ Simple Timeout example (using timeout)
+ Form validation (using .combineLatest)
  + RxTextView.textChanges()发送的第一个元素是空字符串，需要skip
+ Simple and Advanced polling (using interval and repeatWhen)
  + interval repeatWhen
+ Simple and Advanced exponential backoff (using delay and retryWhen)
  + retryWhen实现exponential backoff
+ Persist data on Activity rotations (using Subjects and retained Fragments) ？？？？
+ Pagination with Rx (using Subjects)
  + rxjava填充数据，更新recyclerview

[RxJava2-Android-Samples](https://github.com/amitshekhariitbhu/RxJava2-Android-Samples)

[RxJava: Single, Maybe and Completable](https://android.jlelse.eu/rxjava-single-maybe-and-completable-8686db42bac8)



[关于 RxJava 最友好的文章—— RxJava 2.0 全新来袭](https://juejin.im/post/582b2c818ac24700618ff8f5#heading-7)

[关于RxJava最友好的文章——背压（Backpressure）](https://juejin.im/post/582d413c8ac24700619cceed)