# RecyclerView缓存机制

[RecyclerView 缓存机制 | 如何复用表项？](https://juejin.cn/post/6844903778303344647)

[RecyclerView 缓存机制 | 回收些什么？](https://juejin.cn/post/6844903778303361038)

[RecyclerView 缓存机制 | 回收到哪去？](https://juejin.cn/post/6844903778307538958)

[RecyclerView缓存机制 | scrap view 的生命周期](https://juejin.cn/post/6844903780006264845)

上面四篇很好的解释了缓存机制

[读源码长知识 | 更好的RecyclerView点击监听器](https://juejin.cn/post/6844903862361391117)

+ 层层传递点击监听回调
  + 优点是简单易懂，但缺点是点击事件的接口经过多方传递
  + 还有一个缺点是，内存中会多出 N 个 `OnClickListener` 对象（N为一屏的表项个数）。而且`onBindViewHolder()`会在列表滚动时多次触发，导致会为同一个表项无谓地多次设置点击监听器
  + 还有一个缺点是，内存中会多出 N 个 `OnClickListener` 对象（N为一屏的表项个数）。虽然这也不是一个很大的开销。而且`onBindViewHolder()`会在列表滚动时多次触发，导致会为同一个表项无谓地多次设置点击监听器。
+ 判断点击坐标是否落在表项区域内来获取点击

[更好的 RecyclerView 表项子控件点击监听器](https://juejin.cn/post/6881427923316768776)

+ 层层传递点击事件回调
  + 缺点是：**“对扩展不开放”**。当需求变化时，比如表项新增一个带点击事件的子控件，就必须修改`OnItemClickListener`和`MyViewHolder`
  + 还有一个缺点是：**“增加表项视图层级”**
+ 将触点所在的`RecyclerView`坐标系转换成“表项坐标系”，得到的触点坐标就和表项子控件在同一坐标系中，就能判断触点是否落在子控件矩形区域内
  + 依据name获取id，需要重写setid，这是个小问题

https://github.com/wisdomtl/Layout_DSL

扩展函数的方式很棒

[策略模式应用 | 每当为 RecyclerView 新增类型时就很抓狂](https://juejin.cn/post/6876967151975006221#heading-3)

https://github.com/wisdomtl/VarietyAdapter

`Adapter`难扩展，一扩展就出 bug 的原因是**适配器和具体数据类型耦合**

**构建表项**和**填充表项**这两个抽象的动作，不会随着业务变化而变化的，但**构建什么表项**和**怎么填充表项**是两个具体的动作，会随着业务的变化而变化

声明一组策略，它看上去和`RecyclerView.Adapter`没什么两样，几乎拥有相同的接口，目的是为了把原本`RecyclerView.Adapter`做的事情，由它来代理。但它并没有直接继承`RecyclerView.Adapter`，即它不拥有完整的`RecyclerView.Adapter`的功能，所以不能称为代理模式，而应该是策略模式

很好的解释了代理模式和策略模式的差异

[更高效地刷新 RecyclerView | DiffUtil二次封装](https://juejin.cn/post/6882531923537707015#heading-4)

为了配合VarietyAdapter，继续基类和业务类分离，思路看看就好。使用ListAdapter就好

Payload是用于局部刷新

[换一个思路，超简单的RecyclerView预加载](https://juejin.cn/post/6885146484791050247)

pagings可以

[RecyclerView 动画原理 | 换个姿势看源码（pre-layout）](https://juejin.cn/post/6890288761783975950)

[RecyclerView 动画原理 | pre-layout，post-layout 与 scrap 缓存的关系](https://juejin.cn/post/6892809944702124045)

[RecyclerView 动画原理 | 如何存储并应用动画属性值？](https://juejin.cn/post/6895523568025600014)

