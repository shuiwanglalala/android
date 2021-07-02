# [Kotlin 协程入门这一篇就够了](https://juejin.cn/post/6844903871655968781#heading-2)

## 结构化并发（`Structured concurrency`）

## 协程的泄漏

如何避免泄漏呢？这其实就是`CoroutineScope` 的作用，通过`launch`或者`async`启动一个协程需要指定`CoroutineScope`，当要取消协程的时候只需要调用`CoroutineScope.cancel()` ，kotlin 会帮我们自动取消在这个作用域里面启动的协程

结构化并发可以保证当一个作用域被取消，作用域里面的所有协程会被取消

结构化并发保证当suspend函数返回的时候，函数里面的所有工作都已经完成

当协程出错，调用者或者作用域会收到通知，从而可以进行异常处理