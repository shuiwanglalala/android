# Rxjava Opeartor

https://github.com/KunMinX/RxJava2-Operators-Magician

https://mcxiaoke.gitbooks.io/rxdocs/content/



## 创建操作

用于创建Observable的操作符

- [`Create`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Create.html) — 通过调用观察者的方法从头创建一个Observable
- [`Defer`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Defer.html) — 在观察者订阅之前不创建这个Observable，为每一个观察者创建一个新的Observable
  - [Deferring Observable code until subscription in RxJava](https://blog.danlew.net/2015/07/23/deferring-observable-code-until-subscription-in-rxjava/)
- [`Empty/Never/Throw`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Empty.html) — 创建行为受限的特殊Observable
- [`From`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/From.html) — 将其它的对象或数据结构转换为Observable
- [`Interval`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Interval.html) — 创建一个定时发射整数序列的Observable
- [`Just`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Just.html) — 将对象或者对象集合转换为一个会发射这些对象的Observable
- [`Range`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Range.html) — 创建发射指定范围的整数序列的Observable
- [`Repeat`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Repeat.html) — 创建重复发射特定的数据或数据序列的Observable
  - repeatwhen
    - [Simple and Advanced polling (using interval and repeatWhen)](https://github.com/kaushikgopal/RxJava-Android-Samples)
    - https://blog.danlew.net/2016/01/25/rxjavas-repeatwhen-and-retrywhen-explained/
- [`Start`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Start.html) — 创建发射一个函数的返回值的Observable
- [`Timer`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Timer.html) — 创建在一个指定的延迟之后发射单个数据的Observable

## 变换操作

这些操作符可用于对Observable发射的数据进行变换，详细解释可以看每个操作符的文档

- [`Buffer`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Buffer.html) — 缓存，可以简单的理解为缓存，它定期从Observable收集数据到一个集合，然后把这些数据集合打包发射，而不是一次发射一个
  - [Accumulate calls (using buffer)](https://github.com/kaushikgopal/RxJava-Android-Samples)
- [`FlatMap`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/FlatMap.html) — 扁平映射，将Observable发射的数据变换为Observables集合，然后将这些Observable发射的数据平坦化的放进一个单独的Observable，可以认为是一个将嵌套的数据结构展开的过程
  - FlatMap对这些Observables发射的数据做的是合并(merge)操作，因此它们可能是交错的
  - 如果任何一个通过这个flatMap操作产生的单独的Observable调用onError异常终止了，这个Observable自身会立即调用onError并终止
  - concatMap
  - switchMap
- [`GroupBy`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/GroupBy.html) — 分组，将原来的Observable分拆为Observable集合，将原始Observable发射的数据按Key分组，每一个Observable发射一组不同的数据
- [`Map`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Map.html) — 映射，通过对序列的每一项都应用一个函数变换Observable发射的数据，实质是对序列中的每一项执行一个函数，函数的参数就是这个数据项
- [`Scan`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Scan.html) — 扫描，对Observable发射的每一项数据应用一个函数，然后按顺序依次发射这些值
- [`Window`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Window.html) — 窗口，定期将来自Observable的数据分拆成一些Observable窗口，然后发射这些窗口，而不是每次发射一项。类似于Buffer，但Buffer发射的是数据，Window发射的是Observable，每一个Observable发射原始Observable的数据的一个子集



[如何形象地描述RxJava中的背压和流控机制？](http://zhangtielei.com/posts/blog-rxjava-backpressure.html)



## 过滤操作

这些操作符用于从Observable发射的数据中进行选择

- [`Debounce`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Debounce.html) — 只有在空闲了一段时间后才发射数据，通俗的说，就是如果一段时间没有操作，就执行一次操作
  - [Instant/Auto searching text listeners (using Subjects & debounce)](Instant/Auto searching text listeners (using Subjects & debounce))
- [`Distinct`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Distinct.html) — 去重，过滤掉重复数据项
- [`ElementAt`](https://mcxiaoke.gitbooks.io/rxdocs/content/ElementAt.md) — 取值，取特定位置的数据项
- [`Filter`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Filter.html) — 过滤，过滤掉没有通过谓词测试的数据项，只发射通过测试的
- [`First`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/First.html) — 首项，只发射满足条件的第一条数据
- [`IgnoreElements`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/IgnoreElements.html) — 忽略所有的数据，只保留终止通知(onError或onCompleted)
- [`Last`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Last.html) — 末项，只发射最后一条数据
- [`Sample`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Sample.html) — 取样，定期发射最新的数据，等于是数据抽样，有的实现里叫ThrottleLast
  - ThrottleFirst 点击过滤
- [`Skip`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Skip.html) — 跳过前面的若干项数据
- [`SkipLast`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/SkipLast.html) — 跳过后面的若干项数据
- [`Take`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Take.html) — 只保留前面的若干项数据
- [`TakeLast`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/TakeLast.html) — 只保留后面的若干项数据

## 组合操作

组合操作符用于将多个Observable组合成一个单一的Observable

- [`And/Then/When`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/And.html) — 通过模式(And条件)和计划(Then次序)组合两个或多个Observable发射的数据集
- [`CombineLatest`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/CombineLatest.html) — 当两个Observables中的任何一个发射了一个数据时，通过一个指定的函数组合每个Observable发射的最新数据（一共两个数据），然后发射这个函数的结果
  - [Form validation](https://github.com/kaushikgopal/RxJava-Android-Samples)
- [`Join`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Join.html) — 无论何时，如果一个Observable发射了一个数据项，只要在另一个Observable发射的数据项定义的时间窗口内，就将两个Observable发射的数据合并发射
- [`Merge`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Merge.html) — 将两个Observable发射的数据组合并成一个
  - concat
    - [先读取缓存，如果缓存没数据再通过网络请求获取数据后更新UI](https://www.jianshu.com/p/81fac37430dd)
    - [Pseudo caching : retrieve data first from a cache, then a network call (using concat, concatEager, merge or publish)](https://github.com/kaushikgopal/RxJava-Android-Samples)
- [`StartWith`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/StartWith.html) — 在发射原来的Observable的数据序列之前，先发射一个指定的数据序列或数据项
- [`Switch`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Switch.html) — 将一个发射Observable序列的Observable转换为这样一个Observable：它逐个发射那些Observable最近发射的数据
- [`Zip`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Zip.html) — 打包，使用一个指定的函数将多个Observable发射的数据组合在一起，然后将这个函数的结果作为单项数据发射
  - [RxJava应用场景：使用zip操作符等待多个网络请求完成](http://www.jcodecraeer.com/a/anzhuokaifa/androidkaifa/2016/0325/4080.html)

## 错误处理

这些操作符用于从错误通知中恢复

- [`Catch`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Catch.html) — 捕获，继续序列操作，将错误替换为正常的数据，从onError通知中恢复
- [`Retry`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Retry.html) — 重试，如果Observable发射了一个错误通知，重新订阅它，期待它正常终止
  - retrywhen
    - [Simple and Advanced exponential backoff (using delay and retryWhen)](https://github.com/kaushikgopal/RxJava-Android-Samples)
    - https://stackoverflow.com/questions/22066481/rxjava-can-i-use-retry-but-with-delay/25292833#25292833

## 辅助操作

一组用于处理Observable的操作符

- [`Delay`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Delay.html) — 延迟一段时间发射结果数据
- [`Do`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Do.html) — 注册一个动作占用一些Observable的生命周期事件，相当于Mock某个操作
- [`Materialize/Dematerialize`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Materialize.html) — 将发射的数据和通知都当做数据发射，或者反过来
- [`ObserveOn`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/ObserveOn.html) — 指定观察者观察Observable的调度程序（工作线程）
- [`Serialize`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Serialize.html) — 强制Observable按次序发射数据并且功能是有效的
- [`Subscribe`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Subscribe.html) — 收到Observable发射的数据和通知后执行的操作
- [`SubscribeOn`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/SubscribeOn.html) — 指定Observable应该在哪个调度程序上执行
- [`TimeInterval`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/TimeInterval.html) — 将一个Observable转换为发射两个数据之间所耗费时间的Observable
- [`Timeout`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Timeout.html) — 添加超时机制，如果过了指定的一段时间没有发射数据，就发射一个错误通知
  - 如果网络请求超时没有返回error，timeout能确保返回error
- [`Timestamp`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Timestamp.html) — 给Observable发射的每个数据项添加一个时间戳
- [`Using`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Using.html) — 创建一个只在Observable的生命周期内存在的一次性资源

## 条件和布尔操作

这些操作符可用于单个或多个数据项，也可用于Observable

- [`All`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Conditional.html#All) — 判断Observable发射的所有的数据项是否都满足某个条件
- [`Amb`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Conditional.html#Amb) — 给定多个Observable，只让第一个发射数据的Observable发射全部数据
- [`Contains`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Conditional.html#Contains) — 判断Observable是否会发射一个指定的数据项
- [`DefaultIfEmpty`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Conditional.html#DefaultIfEmpty) — 发射来自原始Observable的数据，如果原始Observable没有发射数据，就发射一个默认数据
- [`SequenceEqual`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Conditional.html#SequenceEqual) — 判断两个Observable是否按相同的数据序列
- [`SkipUntil`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Conditional.html#SkipUntil) — 丢弃原始Observable发射的数据，直到第二个Observable发射了一个数据，然后发射原始Observable的剩余数据
- [`SkipWhile`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Conditional.html#SkipWhile) — 丢弃原始Observable发射的数据，直到一个特定的条件为假，然后发射原始Observable剩余的数据
- [`TakeUntil`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Conditional.html#TakeUntil) — 发射来自原始Observable的数据，直到第二个Observable发射了一个数据或一个通知
- [`TakeWhile`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Conditional.html#TakeWhile) — 发射原始Observable的数据，直到一个特定的条件为真，然后跳过剩余的数据

## 算术和聚合操作

这些操作符可用于整个数据序列

- [`Average`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Mathematical.html#Average) — 计算Observable发射的数据序列的平均值，然后发射这个结果
- [`Concat`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Mathematical.html#Concat) — 不交错的连接多个Observable的数据
- [`Count`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Mathematical.html#Count) — 计算Observable发射的数据个数，然后发射这个结果
- [`Max`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Mathematical.html#Max) — 计算并发射数据序列的最大值
- [`Min`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Mathematical.html#Min) — 计算并发射数据序列的最小值
- [`Reduce`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Mathematical.html#Reduce) — 按顺序对数据序列的每一个应用某个函数，然后返回这个值
- [`Sum`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Mathematical.html#Sum) — 计算并发射数据序列的和

## 连接操作

一些有精确可控的订阅行为的特殊Observable

- [`Connect`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Connect.html) — 指示一个可连接的Observable开始发射数据给订阅者
- [`Publish`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Publish.html) — 将一个普通的Observable转换为可连接的
- [`RefCount`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/RefCount.html) — 使一个可连接的Observable表现得像一个普通的Observable
- [`Replay`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Replay.html) — 确保所有的观察者收到同样的数据序列，即使他们在Observable开始发射数据之后才订阅
  - https://github.com/amitshekhariitbhu/RxJava2-Android-Samples/blob/master/app/src/main/java/com/rxjava2/android/samples/ui/operators/ReplayExampleActivity.java

## 转换操作

- [`To`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/To.html) — 将Observable转换为其它的对象或数据结构
- [`Blocking`](https://mcxiaoke.gitbooks.io/rxdocs/content/operators/Blocking-Observable-Operators.html) 阻塞Observable的操作符



