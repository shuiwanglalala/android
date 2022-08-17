# ViewModel

https://medium.com/androiddevelopers/viewmodels-and-livedata-patterns-antipatterns-21efaef74a54

## ViewModel 的生命周期

[`ViewModel`](https://developer.android.com/reference/androidx/lifecycle/ViewModel?hl=zh-cn) 对象存在的时间范围是获取 [`ViewModel`](https://developer.android.com/reference/androidx/lifecycle/ViewModel?hl=zh-cn) 时传递给 [`ViewModelProvider`](https://developer.android.com/reference/androidx/lifecycle/ViewModelProvider?hl=zh-cn) 的 [`Lifecycle`](https://developer.android.com/reference/androidx/lifecycle/Lifecycle?hl=zh-cn)。[`ViewModel`](https://developer.android.com/reference/androidx/lifecycle/ViewModel?hl=zh-cn) 将一直留在内存中，直到限定其存在时间范围的 [`Lifecycle`](https://developer.android.com/reference/androidx/lifecycle/Lifecycle?hl=zh-cn) 永久消失：对于 Activity，是在 Activity 完成时；而对于 Fragment，是在 Fragment 分离时。

## 在 Fragment 之间共享数据

此方法具有以下优势

- Activity 不需要执行任何操作，也不需要对此通信有任何了解
- 除了 `SharedViewModel` 约定之外，Fragment 不需要相互了解。如果其中一个 Fragment 消失，另一个 Fragment 将继续照常工作
- 每个 Fragment 都有自己的生命周期，而不受另一个 Fragment 的生命周期的影响。如果一个 Fragment 替换另一个 Fragment，界面将继续工作而没有任何问题