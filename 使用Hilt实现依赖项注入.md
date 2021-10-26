# 使用Hilt实现依赖项注入

## Hilt 应用类

所有使用 Hilt 的应用都必须包含一个带有 `@HiltAndroidApp` 注释的 `Application` 类

`@HiltAndroidApp` 会触发 Hilt 的代码生成操作，生成的代码包括应用的一个基类，该基类充当应用级依赖项容器

生成的这一 Hilt 组件会附加到 `Application` 对象的生命周期，并为其提供依赖项。此外，它也是应用的父组件，这意味着，其他组件可以访问它提供的依赖项

## 将依赖项注入 Android 类

在 `Application` 类中设置了 Hilt 且有了应用级组件后，Hilt 可以为带有 `@AndroidEntryPoint` 注释的其他 Android 类提供依赖项

Hilt 目前支持以下 Android 类

- `Application`（通过使用 `@HiltAndroidApp`）
- `Activity`
- `Fragment`
- `View`
- `Service`
- `BroadcastReceiver`

如果您使用 `@AndroidEntryPoint` 为某个 Android 类添加注释，则还必须为依赖于该类的 Android 类添加注释。例如，如果您为某个 Fragment 添加注释，则还必须为使用该 Fragment 的所有 Activity 添加注释

**注意**：在 Hilt 对 Android 类的支持方面还要注意以下几点

- Hilt 仅支持扩展 [`ComponentActivity`](https://developer.android.com/reference/kotlin/androidx/activity/ComponentActivity?hl=zh-cn) 的 Activity，如 [`AppCompatActivity`](https://developer.android.com/reference/kotlin/androidx/appcompat/app/AppCompatActivity?hl=zh-cn)
- Hilt 仅支持扩展 `androidx.Fragment` 的 Fragment
- Hilt 不支持保留的 Fragment

`@AndroidEntryPoint` 会为项目中的每个 Android 类生成一个单独的 Hilt 组件。这些组件可以从它们各自的父类接收依赖项

**注意**：由 Hilt 注入的字段不能为私有字段。尝试使用 Hilt 注入私有字段会导致编译错误

## 定义 Hilt 绑定

“绑定”包含将某个类型的实例作为依赖项提供所需的信息

## Hilt 模块

Hilt 模块是一个带有 `@Module` 注释的类。与 [Dagger 模块](https://developer.android.com/training/dependency-injection/dagger-android?hl=zh-cn#dagger-modules)一样，它会告知 Hilt 如何提供某些类型的实例。与 Dagger 模块不同的是，您必须使用 `@InstallIn` 为 Hilt 模块添加注释，以告知 Hilt 每个模块将用在或安装在哪个 Android 类中

### 使用 @Binds 注入接口实例

`@Binds` 注释会告知 Hilt 在需要提供接口的实例时要使用哪种实现

## 为 Android 类生成的组件

对于您可以从中执行字段注入的每个 Android 类，都有一个关联的 Hilt 组件，您可以在 `@InstallIn` 注释中引用该组件。每个 Hilt 组件负责将其绑定注入相应的 Android 类

**注意**：Hilt 不会为广播接收器生成组件，因为 Hilt 直接从 `ApplicationComponent` 注入广播接收器

### 组件作用域

默认情况下，Hilt 中的所有绑定都未限定作用域。这意味着，每当应用请求绑定时，Hilt 都会创建所需类型的一个新实例

不过，Hilt 也允许将绑定的作用域限定为特定组件。Hilt 只为绑定作用域限定到的组件的每个实例创建一次限定作用域的绑定，对该绑定的所有请求共享同一实例

**注意**：将绑定的作用域限定为某个组件的成本可能很高，因为提供的对象在该组件被销毁之前一直保留在内存中。请在应用中尽量少用限定作用域的绑定。如果绑定的内部状态要求在某一作用域内使用同一实例，或者绑定的创建成本很高，那么将绑定的作用域限定为某个组件是一种恰当的做法

### 组件层次结构

**注意**：默认情况下，如果您在视图中执行字段注入，`ViewComponent` 可以使用 `ActivityComponent` 中定义的绑定。如果您还需要使用 `FragmentComponent` 中定义的绑定并且视图是 Fragment 的一部分，应将 `@WithFragmentBindings` 注释和 `@AndroidEntryPoint` 一起使用

### 组件默认绑定

每个 Hilt 组件都附带一组默认绑定，Hilt 可以将其作为依赖项注入您自己的自定义绑定。请注意，这些绑定对应于常规 Activity 和 Fragment 类型，而不对应于任何特定子类。这是因为，Hilt 会使用单个 Activity 组件定义来注入所有 Activity。每个 Activity 都有此组件的不同实例

还可以使用 `@ApplicationContext` 获得应用上下文绑定

此外，还可以使用 `@ActivityContext` 获得 Activity 上下文绑定

## 在 Hilt 不支持的类中注入依赖项

在这些情况下，您可以使用 `@EntryPoint` 注释创建入口点。入口点是由 Hilt 管理的代码与并非由 Hilt 管理的代码之间的边界。它是代码首次进入 Hilt 所管理对象的图的位置。入口点允许 Hilt 使用它并不管理的代码提供依赖关系图中的依赖项

例如，Hilt 并不直接支持[内容提供程序](https://developer.android.com/guide/topics/providers/content-providers?hl=zh-cn)。如果您希望内容提供程序使用 Hilt 来获取某些依赖项，需要为所需的每个绑定类型定义一个带有 `@EntryPoint` 注释的接口并添加限定符。然后，添加 `@InstallIn` 以指定要在其中安装入口点的组件

如需访问入口点，请使用来自 `EntryPointAccessors` 的适当静态方法。参数应该是组件实例或充当组件持有者的 `@AndroidEntryPoint` 对象。确保您以参数形式传递的组件和 `EntryPointAccessors` 静态方法都与 `@EntryPoint` 接口上的 `@InstallIn` 注释中的 Android 类匹配

## Hilt 和 Dagger

Dagger 和 Hilt 代码可以共存于同一代码库中。不过，在大多数情况下，最好使用 Hilt 管理您在 Android 上对 Dagger 的所有使用