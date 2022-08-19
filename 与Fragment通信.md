# 与Fragment通信

## 使用 `ViewModel` 共享数据

### 在 Fragment 之间共享数据

#### 在父 Fragment 与子 Fragment 之间共享数据

## 使用 Fragment Result API 获取结果

在某些情况下，您可能要在 Fragment 之间或 Fragment 与其宿主 Activity 之间传递一次性值。例如，您可能有一个 fragment，它读取二维码，并将数据传回之前的 fragment。在 fragment 版本 1.3.0 及更高版本中，每个 [`FragmentManager`](https://developer.android.com/reference/androidx/fragment/app/FragmentManager?hl=zh-cn) 都实现了 [`FragmentResultOwner`](https://developer.android.com/reference/androidx/fragment/app/FragmentResultOwner?hl=zh-cn)。这意味着，`FragmentManager` 可以充当 fragment 结果的集中存储区。此更改通过设置 Fragment 结果并监听这些结果而不要求组件直接相互引用，让这些组件能够相互通信。

### 在 Fragment 之间传递结果

对于给定的键，只能有一个监听器和结果。如果您对同一个键多次调用 `setFragmentResult()`，并且监听器未处于 `STARTED` 状态，则系统会将所有待处理的结果替换为更新后的结果。如果您设置的结果没有相应的监听器来接收，则结果会存储在 `FragmentManager` 中，直到您设置一个具有相同键的监听器。监听器收到结果并触发 `onFragmentResult()` 回调后，结果会被清除。这种行为有两个主要影响：

- 返回堆栈上的 Fragment 只有在被弹出且处于 `STARTED` 状态之后才会收到结果。
- 如果在设置结果时监听结果的 Fragment 处于 `STARTED` 状态，则会立即触发监听器的回调。
