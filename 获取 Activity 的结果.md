# 获取 Activity 的结果

+ 准备获取 Activity 结果
  + 如果您有多个使用不同协定或需要单独回调的 Activity 结果调用，则您可以多次调用 prepareCall()，以准备多个 ActivityResultLauncher 实例。每次创建 Fragment 或 Activity 时，都必须按照相同的顺序调用 prepareCall()，才能确保将生成的结果传递给正确的回调
  + 在 Fragment 或 Activity 创建完毕之前可安全地调用 prepareCall()，因此，在为返回的 ActivityResultLauncher 实例声明成员变量时可以直接使用它
    + 虽然在 Fragment 或 Activity 创建完毕之前可安全地调用 prepareCall()，但在 Fragment 或 Activity 的 Lifecycle 变为 CREATED 状态之前，您无法启动 ActivityResultLauncher
+ 在单独的类中接收 Activity 结果
  + 虽然 ComponentActivity 和 Fragment 类通过实现 ActivityResultCaller 接口来允许您使用 prepareCall() API，但您也可以直接使用 ActivityResultRegistry 在未实现 ActivityResultCaller 的单独类中接收结果
  + 使用 ActivityResultRegistry API 时，强烈建议您使用可接受 LifecycleOwner 作为参数的 API，因为 LifecycleOwner 会在 Lifecycle 被销毁时自动移除已注册的启动器





[是时候丢掉 onActivityResult 了 ！](https://juejin.im/post/6844904106528604167)