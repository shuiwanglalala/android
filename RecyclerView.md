# RecyclerView

https://github.com/CymChad/BaseRecyclerViewAdapterHelper

## Google方案

### 多类型

https://medium.com/androiddevelopers/merge-adapters-sequentially-with-mergeadapter-294d2942127a

To support different `ViewHolder` types, you should implement `Adapter.getItemViewType`. When you’re reusing `ViewHolders`, make sure that the same view type doesn’t point to different `ViewHolders`! One best practice for this is to return the layout ID as the view type

+ ViewHolders

ViewHolders

To support different `ViewHolder` types, you should implement `Adapter.getItemViewType`. When you’re reusing `ViewHolders`, make sure that the same view type doesn’t point to different `ViewHolders`! One best practice for this is to return the layout ID as the view type

+ Data changes notifications

prefer more granular updates or use an `Adapter` implementation that does this automatically, like `ListAdapter` or `SortedList`

https://github.com/erikjhordan-rey/RecyclerView-ConcatAdapter

很清爽的例子 ConcatAdapter ListAdapter ViewBinding

## DiffUtil

### ItemDecoration

https://github.com/cabriole/Decorator

### Drag Swipe

https://medium.com/@ipaulpro/drag-and-swipe-with-recyclerview-b9456d2b1aaf

https://medium.com/@ipaulpro/drag-and-swipe-with-recyclerview-6a6f0c422efd

https://github.com/iPaulPro/Android-ItemTouchHelper-Demo

各个细节都说明了，很不错

主动触发拖曳，自定义选中及拖曳的动画

https://github.com/TradeMe/Covert

### Snap

https://github.com/MindorksOpenSource/SnapHelperExample

官方SnapHelper

https://github.com/TakuSemba/MultiSnapRecyclerView

只支持**LinearManger**

https://github.com/rubensousa/GravitySnapHelper

功能最强大

### Selection

https://github.com/afollestad/drag-select-recyclerview

滑动多选

recyclerview-selection官方库

### 动画

https://github.com/wasabeef/recyclerview-animators

简单的动画合集

https://github.com/willowtreeapps/spruce-android

整体性的动画

[GitHub - KunMinX/Linkage-RecyclerView: 即使不用饿了么订餐，也请务必收藏好该库！🔥 一行代码即可接入，二级联动订餐列表。](https://github.com/KunMinX/Linkage-RecyclerView)
