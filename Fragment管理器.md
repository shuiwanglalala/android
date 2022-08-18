# Fragment管理器

## 执行事务

### 有关子 fragment 和同级 fragment 的特殊注意事项

在任何给定的时间点，只允许一个 `FragmentManager` 控制 fragment 返回堆栈。如果应用在屏幕上同时显示多个同级 fragment，或者应用使用子 fragment，则必须指定一个 `FragmentManager` 来处理应用的主要导航。

如需在 fragment 事务内定义主要导航 fragment，请对事务调用 [`setPrimaryNavigationFragment()`](https://developer.android.com/reference/kotlin/androidx/fragment/app/FragmentTransaction?hl=zh-cn#setPrimaryNavigationFragment(androidx.fragment.app.Fragment)) 方法，并传入一个 fragment 的实例，该 fragment 的 `childFragmentManager` 应具有主要控制权。

将导航结构视为一系列层，其中 activity 作为最外层，封装下面的每一层子 fragment。每一层都必须有一个主要导航 fragment。当发生返回事件时，最内层控制导航行为。一旦最内层再也没有可从其弹回的 fragment 事务，控制权就会向外回一层，此过程会一直重复，直至到达 activity 为止。

请注意，当同时显示两个或更多 fragment 时，其中只有一个可以是主要导航 fragment。如果将某个 fragment 设为主要导航 fragment，会移除对先前 fragment 的指定。在上例中，如果您将详情 fragment 设为主要导航 fragment，就会移除对主 fragment 的指定。

## 为 fragment 提供依赖项

当您提交 fragment 事务时，您创建的 fragment 实例就是使用的实例。不过，在[配置更改](https://developer.android.com/guide/topics/resources/runtime-changes?hl=zh-cn)期间，activity 及其所有 fragment 都会被销毁，然后使用最适用的 [Android 资源](https://developer.android.com/guide/topics/resources/providing-resources?hl=zh-cn#BestMatch)重新创建。`FragmentManager` 会为您处理所有这些操作。它会重新创建 fragment 的实例，将其附加到宿主，并重新创建返回堆栈状态。

默认情况下，`FragmentManager` 会使用框架提供的 [`FragmentFactory`](https://developer.android.com/reference/androidx/fragment/app/FragmentFactory?hl=zh-cn) 来实例化 fragment 的新实例。此默认工厂使用反射来查找和调用 fragment 的无参数构造函数。这意味着，您无法使用此默认工厂为 fragment 提供依赖项。这也意味着，默认情况下，在重新创建过程中，不会使用您首次创建 fragment 时所用的任何自定义构造函数。
