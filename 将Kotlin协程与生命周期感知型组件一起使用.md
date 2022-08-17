# 将 Kotlin 协程与生命周期感知型组件一起使用

## 生命周期感知型协程范围

### LifecycleScope

为每个 [`Lifecycle`](https://developer.android.com/topic/libraries/architecture/lifecycle?hl=zh-cn) 对象定义了 `LifecycleScope`。在此范围内启动的协程会在 `Lifecycle` 被销毁时取消。您可以通过 `lifecycle.coroutineScope` 或 `lifecycleOwner.lifecycleScope` 属性访问 `Lifecycle` 的 `CoroutineScope`。

## 可重启生命周期感知型协程

https://medium.com/androiddevelopers/a-safer-way-to-collect-flows-from-android-uis-23080b1f8bda

## 挂起生命周期感知型协程

即使 `CoroutineScope` 提供了适当的方法来自动取消长时间运行的操作，在某些情况下，您可能需要暂停执行代码块（除非 `Lifecycle` 处于特定状态）。例如，如需运行 `FragmentTransaction`，您必须等到 `Lifecycle` 至少为 `STARTED`。对于这些情况，`Lifecycle` 提供了其他方法：`lifecycle.whenCreated`、`lifecycle.whenStarted` 和 `lifecycle.whenResumed`。如果 `Lifecycle` 未至少处于所需的最低状态，则会挂起在这些块内运行的任何协程。

**警告**：倾向于使用 `repeatOnLifecycle` API 收集数据流，而不是在 `launchWhenX` API 内部进行收集。由于后面的 API 会挂起协程，而不是在 `Lifecycle` 处于 `STOPPED` 状态时取消。上游数据流会在后台保持活跃状态，并可能会发出新的项并耗用资源。
