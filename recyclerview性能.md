# recyclerview性能

+ 表项布局的选择

+ RecyclerView can perform several optimizations if it can know in advance that RecyclerView's size is not affected by the adapter contents. RecyclerView can still change its size based on other factors (e.g. its parent's size) but this size calculation cannot depend on the size of its children or contents of its adapter (except the number of items in the adapter)
  
  If your use of RecyclerView falls into this category, set this to {@code true}. It will allow RecyclerView to avoid invalidating the whole layout when its adapter contents change
  
  @param hasFixedSize true if adapter changes cannot affect the size of the RecyclerView

+ 刷新
  
  + payload
  + asyncdiffutil

+ 关闭动画

## blog

[RecyclerView 性能优化 | 把加载表项耗时减半 (一)](https://juejin.cn/post/6939666015500369950)

+ 动态构建布局，弃用 xml

+ 不同的 ViewGroup，不同的 measure + layout 耗时
  
  约束布局在recyclerview里用有性能问题

[RecyclerView 性能优化 | 把加载表项耗时减半 (三)](https://juejin.cn/post/6954892589539524615)

+ 将列表首屏显示的表项合并成一个新的表项类型，以缩短填充表项耗时