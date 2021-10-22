# 在多模块应用中使用Dagger

## 使用 Dagger 子组件进行实现

不错

## 包含动态功能模块时的组件依赖关系

未完全理解

## 最佳做法

- `ApplicationComponent` 应始终位于 `app` 模块中
- 如果您需要在某个模块中执行字段注入，或者需要为应用的特定流程限定对象的范围，请在该模块中创建 Dagger 组件
- 对于要用作实用工具或帮助程序且无需构建图表（这就是您需要 Dagger 组件的原因）的 Gradle 模块，请使用不支持构造函数注入的类的 @Provides 和 @Binds 方法来创建和提供公共 Dagger 模块
- 若要在包含动态功能模块的 Android 应用中使用 Dagger，请使用能够访问 `app` 模块中定义的 `ApplicationComponent` 所提供的依赖项的组件依赖项