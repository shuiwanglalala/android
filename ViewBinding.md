# ViewBinding

## 用法

### 在 Fragment 中使用视图绑定

**注意**：`inflate()` 方法会要求您传入布局膨胀器。如果布局已膨胀，您可以调用绑定类的静态 `bind()` 方法

**注意**：Fragment 的存在时间比其视图长。请务必在 Fragment 的 [`onDestroyView()`](https://developer.android.com/reference/kotlin/androidx/fragment/app/Fragment#ondestroyview) 方法中清除对绑定类实例的所有引用

## 与数据绑定的对比

- **更快的编译速度**
- **易于使用**

考虑到这些因素，在某些情况下，最好在项目中同时使用视图绑定和数据绑定。您可以在需要高级功能的布局中使用数据绑定，而在不需要高级功能的布局中使用视图绑定





[ButterKnife被弃用，ViewBinding才是findView的未来？](https://juejin.cn/post/6900229136199974926#heading-2)

各类绑定的历史变迁

[使用视图绑定替代 findViewById](https://juejin.cn/post/6844904088128192525)

 空安全: 视图绑定会检测某个视图是不是只在一些配置下存在，并依据结果生成带有 @Nullable 注解的属性。所以即使在多种配置下定义的布局文件，视图绑定依然能够保证空安全

数据绑定和视图绑定可以生成同样的组件，它们可以同时工作。在两者都被开启时，使用 标签的布局会由数据绑定来生成绑定对象；而其余的布局则由视图绑定生成绑定对象