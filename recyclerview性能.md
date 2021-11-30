# recyclerview性能

[RecyclerView 性能优化 | 把加载表项耗时减半 (一)](https://juejin.cn/post/6939666015500369950)

+ 动态构建布局，弃用 xml

+ 不同的 ViewGroup，不同的 measure + layout 耗时

  约束布局在recyclerview里用有性能问题

[RecyclerView 性能优化 | 把加载表项耗时减半 (三)](https://juejin.cn/post/6954892589539524615)

+ 将列表首屏显示的表项合并成一个新的表项类型，以缩短填充表项耗时