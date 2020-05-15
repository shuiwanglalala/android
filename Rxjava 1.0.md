# Rxjava 1.0

[给 Android 开发者的 RxJava 详解](https://gank.io/post/560e15be2dca930e00da1083)

[RxJavaSamples](https://github.com/rengwuxian/RxJavaSamples)

+ 几个重要的特点

  + 异步
  + 基于事件
    + 一系列的事件流
    + 事件的分类
      + next
      + complete
      + error
  + 观察者模式
  + 操作符，包括对事件/事件流/Observal的操作

+ 如何设计这些类和接口，达到解耦又满足链式调用

  + Observer
  + Subscription
  + Subscriber
  + Observal
  + Observal.OnSubscribe

+ ```java
  // 注意：这不是 subscribe() 的源码，而是将源码中与性能、兼容性、扩展性有关的代码剔除后的核心代码。
  // 如果需要看源码，可以去 RxJava 的 GitHub 仓库下载。
  public Subscription subscribe(Subscriber subscriber) {
      subscriber.onStart();
      onSubscribe.call(subscriber);
      return subscriber;
  }
  ```

  ```java
  // 注意：这不是 lift() 的源码，而是将源码中与性能、兼容性、扩展性有关的代码剔除后的核心代码。
  // 如果需要看源码，可以去 RxJava 的 GitHub 仓库下载。
  public <R> Observable<R> lift(Operator<? extends R, ? super T> operator) {
      return Observable.create(new OnSubscribe<R>() {
          @Override
          public void call(Subscriber subscriber) {
              Subscriber newSubscriber = operator.call(subscriber);
              newSubscriber.onStart();
              onSubscribe.call(newSubscriber);
          }
      });
  }
  ```

  注意理解这两段代码的不同含义

+ 重点是lift的原理，线程切换的原理



[浅谈RxJava中的线程管理](http://zjutkz.net/2017/04/26/%E6%B5%85%E8%B0%88RxJava%E4%B8%AD%E7%9A%84%E7%BA%BF%E7%A8%8B%E7%AE%A1%E7%90%86/)

