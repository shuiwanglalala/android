# ViewModel

## ViewModel 的生命周期

您通常在系统首次调用 Activity 对象的 `onCreate()` 方法时请求 [`ViewModel`](https://developer.android.com/reference/androidx/lifecycle/ViewModel?hl=zh-cn)。系统可能会在 activity 的整个生命周期内多次调用 `onCreate()`，如在旋转设备屏幕时。[`ViewModel`](https://developer.android.com/reference/androidx/lifecycle/ViewModel?hl=zh-cn) 存在的时间范围是从您首次请求 [`ViewModel`](https://developer.android.com/reference/androidx/lifecycle/ViewModel?hl=zh-cn) 直到 activity 完成并销毁

## 在 Fragment 之间共享数据

此方法具有以下优势

- Activity 不需要执行任何操作，也不需要对此通信有任何了解
- 除了 `SharedViewModel` 约定之外，Fragment 不需要相互了解。如果其中一个 Fragment 消失，另一个 Fragment 将继续照常工作
- 每个 Fragment 都有自己的生命周期，而不受另一个 Fragment 的生命周期的影响。如果一个 Fragment 替换另一个 Fragment，界面将继续工作而没有任何问题









# Question

## 为何引入

[是让人耳目一新的 Jetpack MVVM 精讲啊！](https://juejin.cn/post/6844903976240939021#heading-12)

+ 以注重生命周期的方式存储和管理界面相关的数据
+ 让数据可在发生屏幕旋转等配置更改后继续留存
+ 从界面控制器逻辑中分离出视图数据所有权的操作更容易且更高效（需要个P层类）
+ `ViewModel`在对应的 **作用域** 内保持生命周期内的 **局部单例**，这就引发一个更好用的特性，那就是`Fragment`、`Activity`等UI组件间的通信

## 包结构

## 源码

[从源码看 Jetpack（6）-ViewModel 源码详解](https://juejin.cn/post/6873356946896846856#heading-3)

## 如何使用

[`ViewModel`](https://developer.android.com/reference/androidx/lifecycle/ViewModel?hl=zh-cn) 绝不能引用视图、[`Lifecycle`](https://developer.android.com/reference/androidx/lifecycle/Lifecycle?hl=zh-cn) 或可能存储对 Activity 上下文的引用的任何类

ViewModelProvider 提供的 Factory 接口实现类有两个

- NewInstanceFactory。通过反射来实例化 ViewModel，适用于包含无参构造函数的情况
- AndroidViewModelFactory。通过反射来实例化 ViewModel，适用于构造参数只有一个，且参数类型为 Application 的情况

如果想要通过其它类型的构造函数来初始化 ViewModel 的话，就需要我们自己来实现 `ViewModelProvider.Factory` 接口声明初始化逻辑了

## 如何重构已有的代码

## ktx

## 衍生物有哪些

## 是否有类似的替代物