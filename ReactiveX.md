# ReactiveX

[RxDocs](https://github.com/mcxiaoke/RxDocs)

[The Operators of ReactiveX](http://reactivex.io/documentation/operators.html)

+ Creating Observables
  + Create
    + 谨慎使用，努力合乎规范
  + Defer
    + do not create the Observable until the observer subscribes, and create a fresh Observable for each observer
    + [Deferring Observable code until subscription in RxJava](https://blog.danlew.net/2015/07/23/deferring-observable-code-until-subscription-in-rxjava/)
    + [difference-between-observable-defer-and-observable-create-in-java-rx](https://stackoverflow.com/questions/36313946/difference-between-observable-defer-and-observable-create-in-java-rx)
  + Empty/Never/Throw
  + From
    + convert some other object or data structure into an Observable
  + Just
    + 1-10个参数重载，直接emit参数
    + Just和map合作，代替使用Create
  + Start
    + create an Observable that emits the return value of a function-like directive
    + fromCallable
    + [RxJavaExtensions](https://github.com/akarnokd/RxJavaExtensions#asynchronous-jumpstarting-a-sequence)
  + Interval
    + create an Observable that emits a sequence of integers spaced by a given time interval
  + Timer
    + 与Interval对比，只发送一个元素
  + Range
    + create an Observable that emits a particular range of sequential integers
    + 与Interval对比，数量固定，时间间隔不可设置
  + Repeat
+ Transforming Observables
  + Buffer
    + periodically gather items emitted by an Observable into bundles and emit these bundles rather than emitting the items one at a time
    + 从数量和时间间隔两方面，堆集缓存
    + You can use the Buffer operator to implement backpressure (that is, to cope with an Observable that may produce items too quickly for its observer to consume)
  + Window
    + periodically subdivide items from an Observable into Observable windows and emit these windows rather than emitting the items one at a time
    + Window is similar to Buffer, but rather than emitting packets of items from the source Observable, it emits Observables, each one of which emits a subset of items from the source Observable and then terminates with an onCompleted notification
    + 与Buffer类似，从数量和时间间隔两方面，分割元素
  + GroupBy
    - divide an Observable into a set of Observables（GroupedObservable） that each emit a different subset of items from the original Observable
  + Map
  + Scan accumulator
    + apply a function to each item emitted by an Observable, sequentially, and emit each successive value
  + FlatMap
    + transform the items emitted by an Observable into Observables, then flatten the emissions from those into a single Observable。Note that FlatMap merges the emissions of these Observables, so that they may interleave
    +  there is also an operator that does not interleave the emissions from the transformed Observables, but instead emits these emissions in strict order, often called ConcatMap
+ Filtering Observables
  + Debounce throttleWithTimeout
    + only emit an item from an Observable if a particular timespan has passed without it emitting another item（仅在过了一段指定的时间还没发射数据时才发射一个数据）
  + Sample throttleLast
    + 采样，确保采样间隔内发射一次，不能确保两次发射之间的间隔（每秒采样一次，实际采样时间可为0.9、 1.1、2.5、3.9）
    + throttleFirst
  + Distinct
  + First Last ElementAt
  + Skip SkipLast Take TakeLast
    + 从数量和时间间隔两方面，丢弃/获取元素
+ Combining Observables
  + zip
  + CombineLatest
    + 当两个Observables中的任何一个发射了数据时，使用一个函数结合每个Observable发射的最
      近数据项，并且基于这个函数的结果发射数据
  + Join？？？
  + merge
  + StartWith Concat
  + Switch
    + 将一个发射多个Observables的Observable转换成另一个单独的Observable，后者发射那些
      Observables最近发射的数据项
+ Observable Utility Operators
  + Delay
  + Do
    + doOnComplete
    + doOnError
    + doOnDispose
    + doOnTerminate doAfterTerminate
    + doFinally
    + doOnSubscribe
  + ObserveOn
  + SubscribeOn unsubscribeOn
  + Subscribe foreach
  + To