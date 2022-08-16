# 使用Hilt实现依赖项注入

## 将依赖项注入 Android 类

如果您使用 `@AndroidEntryPoint` 为某个 Android 类添加注释，则还必须为依赖于该类的 Android 类添加注释。例如，如果您为某个 Fragment 添加注释，则还必须为使用该 Fragment 的所有 Activity 添加注释。

**注意**：由 Hilt 注入的字段不能为私有字段。尝试使用 Hilt 注入私有字段会导致编译错误。

Hilt 注入的类可以有同样使用注入的其他基类。如果这些类是抽象类，则它们不需要 `@AndroidEntryPoint` 注释。

## Hilt 模块

### 为同一类型提供多个绑定

最佳做法是，如果您向某个类型添加限定符，应向提供该依赖项的所有可能的方式添加限定符。让基本实现或通用实现不带限定符容易出错，并且可能会导致 Hilt 注入错误的依赖项。

## 为 Android 类生成的组件

https://medium.com/androiddevelopers/scoping-in-android-and-hilt-c2e5222317c0

### 组件默认绑定

每个 Hilt 组件都附带一组默认绑定，Hilt 可以将其作为依赖项注入您自己的自定义绑定。请注意，这些绑定对应于常规 Activity 和 Fragment 类型，而不对应于任何特定子类。这是因为，Hilt 会使用单个 Activity 组件定义来注入所有 Activity。每个 Activity 都有此组件的不同实例。

还可以使用 `@ApplicationContext` 获得应用上下文绑定。

此外，还可以使用 `@ActivityContext` 获得 Activity 上下文绑定。
