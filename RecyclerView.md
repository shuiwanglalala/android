# RecyclerView

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

### Google demo

https://github.com/android/views-widgets-samples/tree/main/RecyclerView

简单使用

https://github.com/android/views-widgets-samples/tree/main/RecyclerViewAnimations

默认动画和自定义动画，注意动画被打断，很详细的ItemAnimator demo

https://github.com/android/views-widgets-samples/tree/main/RecyclerViewKotlin

ListAdapter 的使用，demo一般般

## 其他

### 数据绑定

https://github.com/evant/binding-collection-adapter/

### 动画

https://github.com/wasabeef/recyclerview-animators

简单的动画合集

https://github.com/willowtreeapps/spruce-android

整体性的动画

### Expandable

https://github.com/saket/InboxRecyclerView

expandable descendant navigation 很棒的体验

https://github.com/nikhilpanju/FabFilter

### 特殊类型ui

https://github.com/vipulasri/Timeline-View

https://github.com/fython/MaterialStepperView



































https://github.com/CymChad/BaseRecyclerViewAdapterHelper

动画 header empty 多类型item 分组 node dragAndSwipe

3.x与2.x不兼容，升级风险大

https://www.jianshu.com/p/b343fcff51b0

2.x文档





https://github.com/mikepenz/FastAdapter

异常强大的adapter，貌似功能是最全的

sticky header 多选

https://github.com/davideas/FlexibleAdapter

只看demo，是很不错的，代码暂没时间看

sticky header

https://github.com/h6ah4i/android-advancedrecyclerview

与上面大部分类似 drag swipe expand header 

https://github.com/lisawray/groupie

功能不是很清楚

https://github.com/cymcsg/UltimateRecyclerView

## LayoutManager 

https://github.com/google/flexbox-layout

https://github.com/500px/greedo-layout-for-android

按比例

## ItemDecoration

[Android Recyclerview GridLayoutManager column spacing](https://stackoverflow.com/questions/28531996/android-recyclerview-gridlayoutmanager-column-spacing/30701422#30701422)

https://github.com/yqritc/RecyclerView-FlexibleDivider





## Drag Swipe

https://medium.com/@ipaulpro/drag-and-swipe-with-recyclerview-b9456d2b1aaf

https://github.com/iPaulPro/Android-ItemTouchHelper-Demo

官方出品 ItemTouchHelper

## Snap

[让你明明白白的使用RecyclerView——SnapHelper详解](https://www.jianshu.com/p/e54db232df62)

https://github.com/TakuSemba/MultiSnapRecyclerView

放手后回弹至指定位置 snap

## Selection

长按进入选择status，总感觉不是很实用

[A guide to recyclerview-selection](https://proandroiddev.com/a-guide-to-recyclerview-selection-3ed9f2381504)

https://github.com/marcosholgado/multiselection

kotlin demo

https://github.com/guenodz/recyclerview-selection-demo

java demo

https://github.com/afollestad/drag-select-recyclerview

滑动多选，不错



