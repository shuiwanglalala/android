# RecyclerView

[android-RecyclerView](https://github.com/googlesamples/android-RecyclerView/)

[RecyclerView 必知必会](https://mp.weixin.qq.com/s/CzrKotyupXbYY6EY2HP_dA?)

[Android ListView 与 RecyclerView 对比浅析--缓存机制](https://mp.weixin.qq.com/s?__biz=MzA3NTYzODYzMg==&mid=2653578065&idx=2&sn=25e64a8bb7b5934cf0ce2e49549a80d6&chksm=84b3b156b3c43840061c28869671da915a25cf3be54891f040a3532e1bb17f9d32e244b79e3f&scene=21#wechat_redirect)

列表页展示界面，需要支持动画，或者频繁更新，局部刷新，建议使用RecyclerView，更加强大完善，易扩展；其它情况(如微信卡包列表页)两者都OK，但ListView在使用上会更加方便，快捷

[RecyclerView 性能优化 | 安卓 offer 收割基](https://juejin.im/post/5baedbf05188255c596714ab)

[BaseRecyclerViewAdapterHelper](https://github.com/CymChad/BaseRecyclerViewAdapterHelper)

[RecyclerView剖析](https://blog.csdn.net/qq_23012315/article/details/50807224)

[探究RecyclerView的ViewHolder复用](https://www.jianshu.com/p/d7ec36aa8e4b)

## api

+ ViewHolder
  + getAdapterPosition
    + [RecyclerView.ViewHolder - getLayoutPosition vs getAdapterPosition](https://stackoverflow.com/questions/29684154/recyclerview-viewholder-getlayoutposition-vs-getadapterposition)
  + getLayoutPosition
  + getItemId
  + getItemViewType
+ Adapter
  + onCreateViewHolder(ViewGroup, int)
  + onBindViewHolder(ViewHolder, int)
  + getItemCount
  + getItemViewType
  + registerAdapterDataObserver
  + notifyXXXXX
+ ItemDecoration
  + [Android Recyclerview GridLayoutManager column spacing](https://stackoverflow.com/questions/28531996/android-recyclerview-gridlayoutmanager-column-spacing/30701422#30701422)
+ LayoutManager
  + GridLayoutManager
    + SpanSizeLookup
+ ItemAnimator
  + 在rv.setAdapter()之前调用((SimpleItemAnimator)rv.getItemAnimator()).setSupportsChangeAnimations(false)禁用change动画
+ RecycledViewPool
  + setMaxRecycledViews
+ [setHasFixedSize](https://stackoverflow.com/questions/28709220/understanding-recyclerview-sethasfixedsize)
+ scrollToPosition
+ smoothScrollToPosition
+ getViewTreeObserver

## bug

+ [recyclerview-no-scrollbar-when-overscroll-is-turned-off](https://stackoverflow.com/questions/32575323/recyclerview-no-scrollbar-when-overscroll-is-turned-off)
+ [Why hasn't Google fixed the scrollbar length problem in Android?](https://www.quora.com/Why-hasnt-Google-fixed-the-scrollbar-length-problem-in-Android)