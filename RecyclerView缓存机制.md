# RecyclerView缓存机制

[RecyclerView 缓存机制 | 如何复用表项？](https://juejin.cn/post/6844903778303344647)

[RecyclerView 缓存机制 | 回收些什么？](https://juejin.cn/post/6844903778303361038)

[RecyclerView 缓存机制 | 回收到哪去？](https://juejin.cn/post/6844903778307538958)

[RecyclerView缓存机制 | scrap view 的生命周期](https://juejin.cn/post/6844903780006264845)

**`Recycler`有4个层次用于缓存`ViewHolder`对象，优先级从高到底依次为`ArrayList mAttachedScrap`、`ArrayList mCachedViews`、`ViewCacheExtension mViewCacheExtension`、`RecycledViewPool mRecyclerPool`。如果四层缓存都未命中，则重新创建并绑定`ViewHolder`对象**

**缓存性能：**

| 缓存           | 重新创建`ViewHolder` | 重新绑定数据 |
| -------------- | -------------------- | ------------ |
| mAttachedScrap | false                | false        |
| mCachedViews   | false                | false        |
| mRecyclerPool  | false                | true         |

**缓存容量：**

- `mAttachedScrap`：没有大小限制，但最多包含屏幕可见表项。
- `mCachedViews`：默认大小限制为2，放不下时，按照先进先出原则将最先进入的`ViewHolder`存入回收池以腾出空间。
- `mRecyclerPool`：对`ViewHolder`按`viewType`分类存储（通过`SparseArray`），同类`ViewHolder`存储在默认大小为5的`ArrayList`中。

**缓存用途：**

- `mAttachedScrap`：用于布局过程中屏幕可见表项的回收和复用。
- `mCachedViews`：用于移出屏幕表项的回收和复用，且只能用于指定位置的表项，有点像“回收池预备队列”，即总是先回收到`mCachedViews`，当它放不下的时候，按照先进先出原则将最先进入的`ViewHolder`存入回收池。
- `mRecyclerPool`：用于移出屏幕表项的回收和复用，且只能用于指定`viewType`的表项

**缓存结构：**

- `mAttachedScrap`：`ArrayList`
- `mCachedViews`：`ArrayList`
- `mRecyclerPool`：对`ViewHolder`按`viewType`分类存储在`SparseArray`中，同类`ViewHolder`存储在`ScrapData`中的`ArrayList`中

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

+ `RecyclerView`为了实现表项动画，进行了 2 次布局（预布局 + 后布局），在源码上表现为`LayoutManager.onLayoutChildren()`被调用 2 次

+ 预布局的过程始于`RecyclerView.dispatchLayoutStep1()`，终于`RecyclerView.dispatchLayoutStep2()`

+ 在预布局阶段，循环填充表项时，遇到被移除的或是被更新的表项，则会忽略它占用的空间，多余空间被用来加载额外的表项，这些表项在屏幕之外，本来不会被加载

[RecyclerView 动画原理 | pre-layout，post-layout 与 scrap 缓存的关系](https://juejin.cn/post/6892809944702124045)

在每次向`RecyclerView`填充表项之前都会先清空 LayoutManager 中现存表项，将它们 detach 并同时缓存入 `mAttachedScrap`列表中。在紧接着的填充表项阶段，就立马从`mAttachedScrap`中取出刚被 detach 的表项并重新 attach 它们

[RecyclerView 动画原理 | 如何存储并应用动画属性值？](https://juejin.cn/post/6895523568025600014)

+ RecyclerView 将表项动画数据封装了两层，依次是`ItemHolderInfo`和`InfoRecord`，它们记录了列表预布局和后布局表项的位置信息，即表项矩形区域与列表左上角的相对位置，它还用一个`int`类型的标志位来记录表项经历了哪些布局阶段，以判断表项应该做的动画类型（出现，消失，保持）

+ `InfoRecord`被集中存放在一个商店类`ViewInfoStore`中。所有参与动画的表项的`ViewHolder`与`InfoRecord`都会以键值对的形式存储其中

+ RecyclerView 在布局的第三阶段会遍历商店类中所有的键值对，以`InfoRecord`中的标志位为依据，判断执行哪种动画。表项预布局和后布局的位置信息会一并传递给`RecyclerView.ItemAnimator`，以触发动画

+ `RecyclerView.ItemAnimator`收到动画指令和数据后，又将他们封装为`MoveInfo`，不同类型的动画被存储在不同的`MoveInfo`列表中。然后将执行动画的逻辑抛到 Choreographer 的动画队列中，当下一个垂直同步信号到来时，Choreographer 从动画队列中取出并执行表项动画，执行动画即遍历所有的`MoveInfo`列表，为每一个`MoveInfo`构建 ViewPropertyAnimator 实例并启动动画

[RecyclerView 面试题 | 哪些情况下表项会被回收到缓存池？](https://juejin.cn/post/6930412704578404360/)

表项主动移出屏幕

表项被挤出屏幕

高速缓存命中的 ViewHolder 变脏

mCachedViews 中缓存的表项被删除

所有在 pre-layout 阶段被额外填充的表项，若最终没能在 post-layout 阶段也填充到列表中，就都会被回到到缓存池