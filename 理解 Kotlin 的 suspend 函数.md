# [理解 Kotlin 的 suspend 函数](https://blog.yujinyan.me/posts/understanding-kotlin-suspend-functions/)

## `suspend` 的原理

实现 `suspend` 可以在编译的时候把每个挂起点 🏹 后面的逻辑包在一个 lambda 里面，然后去调用回调 API，最终生成类似嵌套的代码。但这样每一个挂起点在运行时都需要开销一个 lambda 对象。Kotlin 和许多其他语言都采用生成状态机的方式，性能更好

具体来说，编译器看到 `suspend` 关键字会去掉 `suspend` ，给函数添加一个额外的 `Continuation` 参数。这个 `Continuation` 就代表了一个回调

## 使用 `suspend` 函数无须关心线程切换

`suspend` 提供了这样一个**约定(Convention)**：调用这个函数不会阻塞当前调用的线程

这相比 callback 和 RxJava 的 API 是要好很多的。这些异步的 API 最终都得依靠回调，但回调回来在哪个线程需要调用方自己搞清楚，得看这些函数里面是怎么实现的。而有了 `suspend` 不阻塞当前线程的约定，调用方其实无须关心这个函数内部是在哪个线程执行的

# [谈谈 Kotlin 协程的 Context 和 Scope](https://blog.yujinyan.me/posts/kotlin-coroutine-context-scope/#coroutinescope-%E4%B8%8E%E3%80%8C%E7%BB%93%E6%9E%84%E5%8C%96%E5%B9%B6%E5%8F%91%E3%80%8D)

## Context 用于配置协程的属性

### Context 是专门定制的数据结构

**Context 像一个集合（Set）**：这个集合由不同类型的 `Element` 组成。可以通过运算符重载的 add 添加元素，如果添加已经存在的类型的元素则会覆盖

将两个 Context 「+」在一起以后返回的类型是 `CombinedContext`。由于这个集合本身和里面的元素 `CoroutineContext.Element` 都是 `CoroutineContext`，我们在调用 `launch` 这种接收 Context 的函数的时候既可以传单个元素，也可以传组合在一起的 Context，而不需要额外在外面加一个 `listOf` 这样的套子，或者使用 vararg，十分简洁优雅

**Context 是不可变（immutable）的**。对 Context 进行添加或者删除元素的操作都会返回新的 Context 对象。这一性质是协程并发场景下的需要

**Context 又像一个字典（Map）**：每一种类型的 `Element` 都有对应的 `CoroutineContext.Key`，可以通过这个 Key 类型安全地获取到相应类型的 Element

Context 集合和字典的性质确保了 `CombinedContext` 这个集合里**每一种类型 Element 的唯一性**

虽然 Context 用起来像字典和集合，但其**实现却是链表**

由于 Context 中每种类型的 Element 是唯一的，而 Element 类型定义在 Kotlin 协程库（kotlinx.coroutines）内部，其数量是固定的，所以对链表操作的时间复杂度是有上界的。使用自定义的链表来实现 Context 相比使用现成的数据结构可以避免一些额外的开销，对于框架实现来说是非常合理的

### 在协程调用链任意位置获取 Context

在 Kotlin 的 suspend 函数中，我们可以在调用链的任意层级获取 Context（Context propogation）

suspend 函数中的 `coroutineContext` 在没有通过`withContext` 更新 Context 的情况下，和调用方的 Context 是相同的。一种有益的理解是可以想象把调用的 suspend 函数内联（inline) 到这个 suspend 块里面，程序的行为不会发生变化

## CoroutineScope 与「结构化并发」

### 结构化并发 Structured Concurrency

在结构化并发中，所有异步任务都会被约束在一个作用域里面，这个作用域类似于结构化编程中的条件、循环、函数控制体，虽然可能有多个任务并发执行，但最终都会从一个出口出来，符合「黑盒」的性质

### Job 与取消

Kotlin 的协程、 Java 的线程和 Goroutine 都是协作式（cooperative）的，意味着要真正支持取消，协程需要主动地去检查当前的 Job 是不是处于 Active 的状态。这是因为如果子程序可以被突兀地中止，很有可能事情做到一半，损坏数据结构或文件资源等

**在封装出的 suspend 函数内部支持取消， return 是不行的，必须抛 `CancellationException`**。因为 return 以后，控制流正常退回上层函数，可能会继续执行后面的同步语句。当协程被取消后，整个调用链应该立即回退。而 `launch` 的协程块不同于 suspend 函数内部，是协程调用树的根节点，因此可以直接 return 结束协程。

所有 `kotlinx.coroutines` 中的 suspend 函数都支持取消。如果 Job 已取消则会抛出 `CancellationException`

### Job 与协程父子关系

在协程的调用树中，除了调用 suspend 函数之外还有可能开启新的协程。根据结构化并发的思想，父协程必须等待所有子协程结束以后才能结束，因此在创建新的协程 `Job` 时必须以某种形式和父协程建立关联

### Kotlin 协程的结构化并发设计

结构化并发认为应当废弃「非结构化」的、fire-and-forget 的异步 API。`CoroutineScope` 的引入，使结构化并发在 Kotlin 协程 API 中成为了默认行为

根据目前的最佳实践，在 suspend 函数中如果需要开启新的协程，需要先借助 `coroutineScope` 打开一个新的块，这个块包含了一个新的 Job 并限定了所有在其中开启的协程的生命周期：如果代码运行到 `coroutineScope` 块后面，意味着所有在这个块里面的异步任务都已成功结束；如果 `coroutineScope` 中任意一个协程抛出了异常，那么调用栈回退，异常会被传递到 `coroutineScope` 的外层

## Kotlin 协程的两个约定

- 定义在 `CoroutineScope` 上的扩展函数提供了这样的约定（Convention）：这个函数会立即返回，但是函数会开启异步任务，可以理解为这个函数内的子程序和调用方的的代码并发执行
- suspend 函数提供的约定：调用这个函数不会阻塞线程，函数内的子程序执行完毕以后函数才会返回，控制流回到调用方。suspend 函数不应该有开启异步任务的副作用

# [初识 Kotlin Flow](https://blog.yujinyan.me/posts/kotlin-flow-introduction/)

## Flow：可以 suspend 的 Sequence

实际上和 Sequence 一样，Flow 的终端操作符才是驱动整个数据流的“原动力”。如果没有终端操作符，只引用了若干 map、filter 中间操作符，相当于只搭建了一个数据管道，Flow builder 中的代码不会运行，数据不会流动。 这种 Flow 被称作「冷流」

## Flow 的额外保证

### 上下文保存（Context preservation）

所以，**Kotlin 协程库的 Flow 实现会检查 emit 和 collect 在同一个协程里执行**，否则会直接抛出异常

注意，**Flow 禁止的是在不同的协程 emit 数据**，并不是说 Flow 块中不能切换 Context