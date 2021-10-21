# 在Android应用中使用Dagger

## Android 中的 Dagger

有关 Dagger 的一个注意事项是，注入的字段不能为私有字段。这些字段的公开范围必须至少为软件包私有

**注意**：字段注入只能在无法使用构造函数注入的 Android 框架类中使用

### 注入 Activity

使用 Activity 时，应在调用 `super.onCreate()` 之前在 Activity 的 `onCreate()` 方法中注入 Dagger，以避免出现 Fragment 恢复问题。在 `super.onCreate()` 中的恢复阶段，Activity 会附加可能需要访问 Activity 绑定的 Fragment

使用 Fragment 时，应在 Fragment 的 `onAttach()` 方法中注入 Dagger。在这种情况下，此操作可以在调用 `super.onAttach()` 之前或之后完成

### Dagger 作用域

**注意**：使用作用域注释的模块只能在带有相同作用域注释的组件中使用

请注意，在将作用域应用于对象时，不要引发内存泄漏。只要限定作用域的组件在内存中，创建的对象就也在内存中

**注意**：使用构造函数注入（通过 `@Inject`）时，应在类中添加作用域注释；使用 Dagger 模块时，应在 `@Provides` 方法中添加作用域注释