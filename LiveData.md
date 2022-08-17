# LiveData

## 使用 LiveData 对象

**注意**：您可以使用 [`observeForever(Observer)`](https://developer.android.com/reference/androidx/lifecycle/LiveData?hl=zh-cn#observeForever(android.arch.lifecycle.Observer%3CT%3E)) 方法在没有关联的 [`LifecycleOwner`](https://developer.android.com/reference/androidx/lifecycle/LifecycleOwner?hl=zh-cn) 对象的情况下注册一个观察者。在这种情况下，观察者会被视为始终处于活跃状态，因此它始终会收到关于修改的通知。您可以通过调用 [`removeObserver(Observer)`](https://developer.android.com/reference/androidx/lifecycle/LiveData?hl=zh-cn#removeObserver(android.arch.lifecycle.Observer%3CT%3E)) 方法来移除这些观察者。

### 观察 LiveData 对象

在大多数情况下，应用组件的 `onCreate()` 方法是开始观察 [`LiveData`](https://developer.android.com/reference/androidx/lifecycle/LiveData?hl=zh-cn) 对象的正确着手点。

通常，LiveData 仅在数据发生更改时才发送更新，并且仅发送给活跃观察者。此行为的一种例外情况是，观察者从非活跃状态更改为活跃状态时也会收到更新。此外，如果观察者第二次从非活跃状态更改为活跃状态，则只有在自上次变为活跃状态以来值发生了更改时，它才会收到更新

## 
