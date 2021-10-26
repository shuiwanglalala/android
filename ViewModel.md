# ViewModel

[ViewModel 和 LiveData：模式 + 反模式](https://medium.com/androiddevelopers/viewmodels-and-livedata-patterns-antipatterns-21efaef74a54)

+ A general rule of thumb is to make sure there are no `android.*` imports in your ViewModels (with exceptions like` android.arch.*`)

+ Conditional statements, loops and general decisions should be done in ViewModels or other layers of an app, not in the Activities or Fragments

  *Keep the logic in Activities and Fragments to a minimum*

+  *Avoid references to Views in ViewModels*

+  *Instead of pushing data to the UI, let the UI observe changes to it*

+ Fat ViewModels

  + Moving some logic out to a presenter, with the same scope as the ViewModel
  + Adding a Domain layer and adopting [Clean Architecture](https://8thlight.com/blog/uncle-bob/2012/08/13/the-clean-architecture.html)

+ *Add a data repository as the single-point entry to your data*

+ *Expose information about the state of your data using a wrapper or another LiveData*

+ Saving activity state

+ An event is something that happens once

  [LiveData with SnackBar, Navigation and other events (the SingleLiveEvent case)](https://medium.com/androiddevelopers/livedata-with-snackbar-navigation-and-other-events-the-singleliveevent-case-ac2622673150)

  https://github.com/KunMinX/UnPeek-LiveData

+ Leaking ViewModels
  + **With ViewModel.onCleared()** you can tell the repository to drop the callback to the ViewModel
  + In the repository you can use a **WeakReference** or you can use an **Event Bus** (both easy to misuse and even considered harmful)
  + Use the LiveData to communicate between the Repository and ViewModel in a similar way to using LiveData between the View and the ViewModel

+ **LiveData in repositories **

  *Whenever you think you need a* [Lifecycle](https://developer.android.com/reference/android/arch/lifecycle/Lifecycle.html) *object inside a* [ViewModel](https://developer.android.com/reference/android/arch/lifecycle/ViewModel.html)*, a* [Transformation](https://developer.android.com/topic/libraries/architecture/livedata#transform_livedata) *is probably the solution*

  已被遗弃，改为flow

+ **Extending LiveData**

  *You don’t usually extend LiveData. Let your activity or fragment tell the ViewModel when it’s time to start loading data*









## ViewModel 的生命周期

您通常在系统首次调用 Activity 对象的 `onCreate()` 方法时请求 [`ViewModel`](https://developer.android.com/reference/androidx/lifecycle/ViewModel?hl=zh-cn)。系统可能会在 activity 的整个生命周期内多次调用 `onCreate()`，如在旋转设备屏幕时。[`ViewModel`](https://developer.android.com/reference/androidx/lifecycle/ViewModel?hl=zh-cn) 存在的时间范围是从您首次请求 [`ViewModel`](https://developer.android.com/reference/androidx/lifecycle/ViewModel?hl=zh-cn) 直到 activity 完成并销毁

**Fragment对应ViewModel的生命周期是怎样的？？**

## 在 Fragment 之间共享数据

此方法具有以下优势

- Activity 不需要执行任何操作，也不需要对此通信有任何了解
- 除了 `SharedViewModel` 约定之外，Fragment 不需要相互了解。如果其中一个 Fragment 消失，另一个 Fragment 将继续照常工作
- 每个 Fragment 都有自己的生命周期，而不受另一个 Fragment 的生命周期的影响。如果一个 Fragment 替换另一个 Fragment，界面将继续工作而没有任何问题









# Question

## 为何引入

+ 以注重生命周期的方式存储和管理界面相关的数据
+ 让数据可在发生屏幕旋转等配置更改后继续留存
+ 从界面控制器逻辑中分离出视图数据所有权的操作更容易且更高效（需要个P层类）
+ `ViewModel`在对应的 **作用域** 内保持生命周期内的 **局部单例**，这就引发一个更好用的特性，那就是`Fragment`、`Activity`等UI组件间的通信（目前看来是最好的通信方式）

[是让人耳目一新的 Jetpack MVVM 精讲啊！](https://juejin.cn/post/6844903976240939021#heading-12)

## 包结构

+ lifecycle-viewmodel
+ lifecycle-viewmodel-ktx

## 源码

[从源码看 Jetpack（6）-ViewModel 源码详解](https://juejin.cn/post/6873356946896846856#heading-3)

## 如何使用

[`ViewModel`](https://developer.android.com/reference/androidx/lifecycle/ViewModel?hl=zh-cn) 绝不能引用视图、[`Lifecycle`](https://developer.android.com/reference/androidx/lifecycle/Lifecycle?hl=zh-cn) 或可能存储对 Activity 上下文的引用的任何类

ViewModelProvider 提供的 Factory 接口实现类有两个

- NewInstanceFactory。通过反射来实例化 ViewModel，适用于包含无参构造函数的情况
- AndroidViewModelFactory。通过反射来实例化 ViewModel，适用于构造参数只有一个，且参数类型为 Application 的情况

如果想要通过其它类型的构造函数来初始化 ViewModel 的话，就需要我们自己来实现 `ViewModelProvider.Factory` 接口声明初始化逻辑了，但可以使用hilt依赖注入

## 如何重构已有的代码

## ktx

## 衍生物有哪些

## 是否有类似的替代物

[Android官方架构组件ViewModel:从前世今生到追本溯源](https://juejin.cn/post/6844903729414537223#heading-1)

源码部分老旧，可以pass

替代了之前的P层