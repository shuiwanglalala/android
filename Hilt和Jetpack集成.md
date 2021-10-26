# Hilt和Jetpack集成

## 使用 Hilt 注入 ViewModel 对象

在 `ViewModel` 对象的构造函数中使用 `@ViewModelInject` 注释来提供一个 [`ViewModel`](https://developer.android.com/topic/libraries/architecture/viewmodel?hl=zh-cn)。您还必须使用 `@Assisted` 为 `SavedStateHandle` 依赖项添加注释

然后，带有 `@AndroidEntryPoint` 注释的 Activity 或 Fragment 可以使用 `ViewModelProvider` 或 `by viewModels()` [KTX 扩展](https://developer.android.com/kotlin/ktx?hl=zh-cn)照常获取 `ViewModel` 实例