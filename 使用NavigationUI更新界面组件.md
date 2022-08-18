# 使用NavigationUI更新界面组件

## 监听导航事件

`NavController` 提供 `OnDestinationChangedListener` 接口，该接口在 `NavController` 的[当前目的地](https://developer.android.com/reference/androidx/navigation/NavController?hl=zh-cn#getCurrentDestination())或其参数发生更改时调用。可以通过 [`addOnDestinationChangedListener()`](https://developer.android.com/reference/androidx/navigation/NavController?hl=zh-cn#addOnDestinationChangedListener(androidx.navigation.NavController.OnDestinationChangedListener)) 方法注册新监听器。请注意，调用 `addOnDestinationChangedListener()` 时，如果当前目的地存在，则会立即被发送到您的监听器。

### 基于参数的监听器

作为替代方案，您还可以将参数与导航图中的默认值结合使用，相应的界面控制器可以使用这些值来更新其状态。
