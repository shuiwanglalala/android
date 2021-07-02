# [一文快速入门 Kotlin 协程](https://juejin.cn/post/6908271959381901325#heading-1)

### CoroutineScope

#### runBlocking

runBlocking 的一个方便之处就是：只有当内部**相同作用域**的所有协程都运行结束后，声明在 runBlocking 之后的代码才能执行，即 runBlocking 会阻塞其所在线程

#### coroutineScope

`coroutineScope` 函数用于创建一个独立的协程作用域，直到所有启动的协程都完成后才结束自身。`runBlocking` 和 `coroutineScope` 看起来很像，因为它们都需要等待其内部所有相同作用域的协程结束后才会结束自己。两者的主要区别在于 `runBlocking` 方法会阻塞当前线程，而 `coroutineScope`不会阻塞线程，而是会挂起并释放底层线程以供其它协程使用。由于这个差别，`runBlocking` 是一个普通函数，而 `coroutineScope` 是一个挂起函数

#### supervisorScope

`supervisorScope` 函数用于创建一个使用了 SupervisorJob 的 coroutineScope，该作用域的特点就是抛出的异常不会连锁取消同级协程和父协程

### CoroutineBuilder

#### launch

`launch` 是一个作用于 CoroutineScope 的扩展函数，用于在不阻塞当前线程的情况下启动一个协程，并返回对该协程任务的引用，即 Job 对象

#### async

`async` 也是一个作用于 CoroutineScope 的扩展函数，和 `launch` 的区别主要就在于：`async` 可以返回协程的执行结果，而 `launch` 不行

#### async 并行分解

由 `suspend` 函数启动的所有协程都必须在该函数返回结果时停止，因此你可能需要保证这些协程在返回结果之前完成。借助 Kotlin 中的结构化并发机制，你可以定义用于启动一个或多个协程的 `coroutineScope`。然后，你可以使用 `await()`（针对单个协程）或 `awaitAll()`（针对多个协程）保证这些协程在从函数返回结果之前完成

### CoroutineContext

#### Job

协程中的 Job 是其上下文 CoroutineContext 中的一部分，可以通过 `coroutineContext[Job]` 表达式从上下文中获取到

#### CoroutineDispatcher

在 Kotlin 中，所有协程都必须在 CoroutineDispatcher 中运行，即使它们在主线程上运行也是如此。协程可以自行暂停，而 CoroutineDispatcher 负责将其恢复

Kotlin 协程库提供了四个 Dispatcher 用于指定在何处运行协程，大部分情况下我们只会接触以下三个

- **Dispatchers.Main** - 使用此调度程序可在 Android 主线程上运行协程。此调度程序只能用于与界面交互和执行快速工作。示例包括调用 `suspend` 函数、运行 Android 界面框架操作，以及更新 [`LiveData`](https://developer.android.google.cn/topic/libraries/architecture/livedata) 对象
- **[Dispatchers.IO](http://Dispatchers.IO)** - 此调度程序经过了专门优化，适合在主线程之外执行磁盘或网络 I/O。示例包括使用 [Room 组件](https://developer.android.google.cn/topic/libraries/architecture/room)、从文件中读取数据或向文件中写入数据，以及运行任何网络操作
- **Dispatchers.Default** - 此调度程序经过了专门优化，适合在主线程之外执行占用大量 CPU 资源的工作。用例示例包括对列表排序和解析 JSON

当 `launch {...}` 在不带参数的情况下使用时，它从外部的协程作用域继承上下文和调度器。而在 GlobalScope 中启动协程时默认使用的调度器是 Dispatchers.default，并使用共享的后台线程池。`newSingleThreadContext` 用于为协程专门创建一个新的线程来运行，专用线程是一种成本非常昂贵的资源，在实际的应用程序中必须在不再需要时释放掉，或者存储在顶级变量中以便在整个应用程序中进行重用

借助协程，你可以细粒度地来调度线程。由于`withContext()`支持让你在不引入回调的情况下控制任何代码的执行线程池，因此你可以将其应用于非常小的函数，例如从数据库中读取数据或执行网络请求。一种不错的做法是使用 `withContext()` 来确保每个函数都是主线程安全的，这意味着，你可以从主线程调用每个函数。这样，调用方就从不需要考虑应该使用哪个线程来执行函数了

#### 组合上下文元素

有时我们需要为协程上下文定义多个元素，那就可以用 `+` 运算符

此外，由于 CoroutineContext 是由一组元素组成的，所以加号右侧的元素会覆盖加号左侧的元素，进而组成新创建的 CoroutineContext

### 取消协程

`job.cancel()`就用于取消协程，`job.join()`用于阻塞等待协程运行结束。因为 `cancel()` 函数调用后会马上返回而不是等待协程结束后再返回，所以此时协程不一定就是已经停止运行了。如果需要确保协程结束运行后再执行后续代码，就需要调用 `join()` 方法来阻塞等待。也可以通过调用 Job 的扩展函数 `cancelAndJoin()` 来完成相同操作，它结合了 `cancel` 和 `join`两个操作

#### 协程可能无法取消

并不是所有协程都可以响应取消操作，协程的取消操作是需要协作(cooperative)完成的，协程必须协作才能取消。协程库中的所有挂起函数都是可取消的，它们在运行时会检查协程是否被取消了，并在取消时抛出 CancellationException 从而结束整个任务

取消协程这个操作类似于在 Java 中调用`Thread.interrupt()`方法来向线程发起中断请求，这两个操作都不会强制停止协程和线程，外部只是相当于发起一个停止运行的请求，需要依靠协程和线程响应请求后主动停止运行。Kotlin 和 Java 之所以均没有提供一个可以直接强制停止协程或线程的方法，是因为这个操作可能会带来各种意想不到的情况。在停止协程和线程的时候，它们可能还持有着某些排他性资源（例如：锁，数据库链接），如果强制性地停止，它们持有的锁就会一直无法得到释放，导致其他协程和线程一直无法得到目标资源，最终可能导致线程死锁。所以`Thread.stop()`方法目前也是处于废弃状态，Java 官方并没有提供可靠的停止线程的方法

#### 用 finally 释放资源

可取消的挂起函数在取消时会抛出 CancellationException，可以依靠`try {...} finally {...}` 或者 Kotlin 的 `use` 函数在取消协程后释放持有的资源

#### NonCancellable

#### 父协程和子协程

当一个协程在另外一个协程的协程作用域中启动时，它将通过 `CoroutineScope.coroutineContext` 继承其上下文，新启动的协程就被称为子协程，子协程的 Job 将成为父协程 Job 的子 Job。父协程总是会等待其所有子协程都完成后才结束自身，所以父协程不必显式跟踪它启动的所有子协程，也不必使用 `Job.join` 在末尾等待子协程完成

#### 传播取消操作

一般情况下，协程的取消操作会通过协程的层次结构来进行传播。如果取消父协程或者父协程抛出异常，那么子协程都会被取消。而如果子协程被取消，则不会影响同级协程和父协程，但如果子协程抛出异常则也会导致同级协程和父协程被取消

#### withTimeout

`withTimeout` 函数用于指定协程的运行超时时间，如果超时则会抛出 TimeoutCancellationException，从而令协程结束运行

如果不希望因为异常导致协程结束，可以改用`withTimeoutOrNull`方法，如果超时就会返回 null

### 异常处理

当一个协程由于异常而运行失败时，它会传播这个异常并传递给它的父协程。接下来，父协程会进行下面几步操作：

- 取消它自己的子级
- 取消它自己
- 将异常传播并传递给它的父级

异常会到达层级的根部，而且当前 CoroutineScope 所启动的所有协程都会被取消

launch 将异常视为未捕获异常，类似于 Java 的 Thread.uncaughtExceptionHandler，当发现异常时就会马上抛出。async 期望最终是通过调用 await 来获取结果 (或者异常)，所以默认情况下它不会抛出异常。这意味着如果使用 async 启动新的协程，它会静默地将异常丢弃，直到调用 `async.await()` 才会得到目标值或者抛出存在的异常

#### CoroutineExceptionHandler

如果不想将所有的异常信息都打印到控制台上，那么可以使用 CoroutineExceptionHandler 作为协程的上下文元素之一，在这里进行自定义日志记录或异常处理，它类似于对线程使用 Thread.uncaughtExceptionHandler。但是，CoroutineExceptionHandler 只会在预计不会由用户处理的异常上调用，因此在 async 中使用它没有任何效果，当 async 内部发生了异常且没有捕获时，那么调用 `async.await()` 依然会导致应用崩溃

#### SupervisorJob

SupervisorJob 来实现上述效果，它类似于常规的 Job，唯一的区别就是取消操作只会向下传播，一个子协程的运行失败不会影响到其他子协程

但是，如果异常没有被处理且 CoroutineContext 没有包含一个 CoroutineExceptionHandler 的话，异常会到达默认线程的 ExceptionHandler。在 JVM 中，异常会被打印在控制台；而在 Android 中，无论异常在那个 Dispatcher 中发生，都会直接导致应用崩溃