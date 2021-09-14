# Lifecycle

## Lifecycle

CREATED状态应该是分开为两端的。某一时刻应该只能处于一种状态

### 实现自定义 LifecycleOwner

```kotlin
class MyActivity : Activity(), LifecycleOwner {

    private lateinit var lifecycleRegistry: LifecycleRegistry

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        lifecycleRegistry = LifecycleRegistry(this)
        lifecycleRegistry.markState(Lifecycle.State.CREATED)
    }

    public override fun onStart() {
        super.onStart()
        lifecycleRegistry.markState(Lifecycle.State.STARTED)
    }

    override fun getLifecycle(): Lifecycle {
        return lifecycleRegistry
    }
}
```





# Question

## 为何引入

+ 生命周期感知型组件可执行操作来响应另一个组件（如 Activity 和 Fragment）的生命周期状态的变化。这些组件有助于您编写出更有条理且往往更精简的代码，此类代码更易于维护

  一种常见的模式是在 Activity 和 Fragment 的生命周期方法中实现依赖组件的操作。但是，这种模式会导致代码条理性很差而且会扩散错误。通过使用生命周期感知型组件，您可以将依赖组件的代码从生命周期方法移入组件本身中

+ 无法保证组件会在 Activity 或 Fragment 停止之前启动。在我们需要执行长时间运行的操作（如 `onStart()` 中的某种配置检查）时尤其如此。这可能会导致出现一种竞态条件，在这种条件下，`onStop()` 方法会在 `onStart()` 之前结束，这使得组件留存的时间比所需的时间要长

## 包结构

+ lifecycle-runtime-ktx
  + lifecycle-common
  + lifecycle-runtime
  + lifecycle-runtime-ktx
+ lifecycle-common-java8
+ lifecycle-service
+ lifecycle-process

## 源码

[从源码看 Jetpack（1）-Lifecycle 源码详解](https://juejin.cn/post/6847902220755992589#heading-16)

## 如何使用

```kotlin
class MyObserver : LifecycleObserver {

    @OnLifecycleEvent(Lifecycle.Event.ON_RESUME)
    fun connectListener() {
        ...
    }

    @OnLifecycleEvent(Lifecycle.Event.ON_PAUSE)
    fun disconnectListener() {
        ...
    }
}

myLifecycleOwner.getLifecycle().addObserver(MyObserver())
```

### 相关的接口

LifecycleObserver

+ FullLifecycleObserver
  + DefaultLifecycleObserver
+ LifecycleEventObserver

LifecycleObserver 是一个空接口，大部分情况下真正具有使用意义的是它的子接口 ，LifecycleObserver 可以说仅是用于类型标记

LifecycleEventObserver 用于监听 Lifecycle 的生命周期变化，可以获取到生命周期事件发生的具体变化

DefaultLifecycleObserver 对父接口的所有方法都进行了默认实现。大多数情况下我们只需要一两种生命周期事件的通知，DefaultLifecycleObserver 的存在就使得我们可以按需重写父接口的方法而无需实现所有抽象方法。而接口可以声明默认方法这一特性是从 Java 8 开始才有的，所以只有当你的项目是以 Java 8 作为目标编译版本时才可以使用 DefaultLifecycleObserver。如果使用 FullLifecycleObserver 的话我们就必须实现所有抽象方法

Google 官方也建议开发者尽量使用 DefaultLifecycleObserver ，因为 Java 8 最终是会成为 Android 开发的主流，而 Java 7 平台下通过注解来实现生命周期回调的方式最终会被废弃

## 如何重构已有的代码

## ktx

## 衍生物有哪些

[从源码看 Jetpack（2）-Lifecycle 衍生物源码详解](https://juejin.cn/post/6847902220760203277)

LifecycleService

ProcessLifecycleOwner

如果app是单进程的，使用lifecycle-process是完全ok的，但是假如一个app有多进程，好像无效

## 是否有类似的替代物







