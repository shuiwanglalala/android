# LiveData

## 使用 LiveData 对象

### 观察 LiveData 对象

通常，LiveData 仅在数据发生更改时才发送更新，并且仅发送给活跃观察者。此行为的一种例外情况是，观察者从非活跃状态更改为活跃状态时也会收到更新。此外，如果观察者第二次从非活跃状态更改为活跃状态，则只有在自上次变为活跃状态以来值发生了更改时，它才会收到更新

## 应用架构中的 LiveData

您可能会想在数据层类中使用 `LiveData` 对象，但 `LiveData` 并不适合处理异步数据流。虽然您可以使用 `LiveData` 转换和 [`MediatorLiveData`](https://developer.android.com/reference/android/arch/lifecycle/MediatorLiveData?hl=zh-cn) 来实现此目的，**但此方法的缺点在于：用于组合数据流的功能非常有限，并且所有 `LiveData` 对象（包括通过转换创建的对象）都会在主线程中观察到**

如果您需要在应用的其他层中使用数据流，请考虑使用 [Kotlin Flow](https://developer.android.com/kotlin/flow?hl=zh-cn)，然后使用 [`asLiveData()`](https://developer.android.com/reference/kotlin/androidx/lifecycle/package-summary?hl=zh-cn#aslivedata) 在 `ViewModel` 中将 Kotlin Flow 转换成 `LiveData`。对于使用 Java 构建的代码库，请考虑将[执行器](https://developer.android.com/guide/background/threading?hl=zh-cn)与回调或 `RxJava` 结合使用

## 扩展 LiveData

+ 您可以使用单例模式扩展 [`LiveData`](https://developer.android.com/reference/androidx/lifecycle/LiveData?hl=zh-cn) 对象以封装系统服务，以便在应用中共享它们。`LiveData` 对象连接到系统服务一次，然后需要相应资源的任何观察者只需观察 `LiveData` 对象

  **这类case，实际中遇见的概率应该不高**

+ 如果服务不需要共享，则可使用lifecycle

## 转换 LiveData

您可以使用转换方法在观察者的生命周期内传送信息。除非观察者正在观察返回的 `LiveData` 对象，否则不会计算转换。因为转换是以延迟的方式计算，所以与生命周期相关的行为会隐式传递下去，而不需要额外的显式调用或依赖项

demo不错



# Question

## 为何引入

+ **确保界面符合数据状态**

  LiveData 遵循观察者模式。当底层数据发生变化时，LiveData 会通知 [`Observer`](https://developer.android.com/reference/androidx/lifecycle/Observer?hl=zh-cn) 对象。您可以整合代码以在这些 `Observer` 对象中更新界面。这样一来，您无需在每次应用数据发生变化时更新界面，因为观察者会替您完成更新

+ **不会发生内存泄漏**

  观察者会绑定到 [`Lifecycle`](https://developer.android.com/reference/androidx/lifecycle/Lifecycle?hl=zh-cn) 对象，并在其关联的生命周期遭到销毁后进行自我清理

+ **不会因 Activity 停止而导致崩溃**

  如果观察者的生命周期处于非活跃状态（如返回栈中的 Activity），则它不会接收任何 LiveData 事件

+ **不再需要手动处理生命周期**

  界面组件只是观察相关数据，不会停止或恢复观察。LiveData 将自动管理所有这些操作，因为它在观察时可以感知相关的生命周期状态变化

+ **数据始终保持最新状态**

  如果生命周期变为非活跃状态，它会在再次变为活跃状态时接收最新的数据。例如，曾经在后台的 Activity 会在返回前台后立即接收最新的数据

+ **适当的配置更改**

  如果由于配置更改（如设备旋转）而重新创建了 Activity 或 Fragment，它会立即接收最新的可用数据

+ **共享资源**

  您可以使用单例模式扩展 [`LiveData`](https://developer.android.com/reference/androidx/lifecycle/LiveData?hl=zh-cn) 对象以封装系统服务，以便在应用中共享它们。`LiveData` 对象连接到系统服务一次，然后需要相应资源的任何观察者只需观察 `LiveData` 对象

## 包结构

## 源码

[从源码看 Jetpack（3）-LiveData 源码详解](https://juejin.cn/post/6847902222345633806)

## 如何使用

[LiveData beyond the ViewModel — Reactive patterns using Transformations and MediatorLiveData](https://medium.com/androiddevelopers/livedata-beyond-the-viewmodel-reactive-patterns-using-transformations-and-mediatorlivedata-fda520ba00b7)

+ One-to-one static transformation — map
+ One-to-one dynamic transformation — switchMap
+ One-to-many dependency — MediatorLiveData

If a component of your app has no connection to the UI, it probably doesn’t need LiveData

Antipattern: Sharing instances of LiveData **这一部分值得深思**

Don’t use Livedata in a var. Wire transformations on initialization



最开始时遇到的一些问题

+ 如何在repo中使用livedata
+ livedata配合retrofit room
+ 如何创建livedata

## 如何重构已有的代码

## ktx

https://github.com/android/architecture-components-samples/tree/main/LiveDataSample

nice demo

To make one LiveData depend on the value of another, you use Transformations or the generic MediatorLiveData class. Transformations, like `map` and `switchMap`, are computed in the main thread. However, using a combination of `switchMap` and the `liveData` builder, you can easily call suspend functions or move the transformation to a different thread

https://stackoverflow.com/questions/57698932/livedatascope-vs-viewmodelscope-in-android

## 衍生物有哪些

## 是否有类似的替代物

livedata的局限性

