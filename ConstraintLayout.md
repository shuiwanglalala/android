# ConstraintLayout

[约束布局ConstraintLayout看这一篇就够了](https://www.jianshu.com/p/17ec9bd6ca8a)

+ layout_constraintBaseline_toBaselineOf
  + 文本基线对齐
+ layout_constraintCircle
+ layout_marginStart
  + 要实现margin，必须先约束该控件在ConstraintLayout里的位置
  + margin只能大于等于0
+ layout_goneMarginStart
  + 约束对象gone后，margin才有效
+ layout_constraintHorizontal_bias
+ 官方不推荐在ConstraintLayout中使用match_parent，可以设置 0dp (MATCH_CONSTRAINT) 配合约束代替match_parent
+ layout_constraintDimensionRatio
  + 当宽或高至少有一个尺寸被设置为0dp时，可以通过属性layout_constraintDimensionRatio设置宽高比
  + app:layout_constraintDimensionRatio="H,2:3"指的是 高:宽=2:3
+ layout_constraintHorizontal_chainStyle
  + CHAIN_SPREAD —— 展开元素 (默认)
  + CHAIN_SPREAD_INSIDE —— 展开元素，但链的两端贴近parent
  + CHAIN_PACKED —— 链的元素将被打包在一起
  + layout_constraintHorizontal_weight
+ Barrier
  + app:barrierDirection
  + app:constraint_referenced_ids
+ Group
  + app:constraint_referenced_ids
  + [Can't set visibility on constraint group](https://stackoverflow.com/questions/47865436/cant-set-visibility-on-constraint-group)
+ Placeholder
  + app:content
+ Guideline
  + layout_constraintGuide_begin
  + layout_constraintGuide_percent

[ConstraintLayout: NEVER EVER!](https://medium.com/@jemli.idea/constraintlayout-never-ever-97c121286100)

NEVER EVER nest ViewGroups inside ConstraintLayout! This is a contradiction in itself and it’s so against what the library was created for at the first place

[万字长文 - 史上最全ConstraintLayout（约束布局）使用详解](https://juejin.cn/post/6949186887609221133#heading-1)

+ 1.3.2 0dp(MATCH_CONSTRAINT)

设置view的大小除了传统的wrap_content、指定尺寸、match_parent外，ConstraintLayout还可以设置为0dp（MATCH_CONSTRAINT），并且0dp的作用会根据设置的类型而产生不同的作用，进行设置类型的属性是layout_constraintWidth_default和layout_constraintHeight_default，取值可为spread、percent、wrap

+ 1.4 Chains(链)

`Chains(链)`还支持`weight（权重）`的配置，使用`layout_constraintHorizontal_weight`和`layout_constraintVertical_weight`进行设置链元素的权重

+ 2.5 Flow（流式虚拟布局）

类似flexboxlayout

+ 2.6 Layer（层布局）

`Layer`继承自`ConstraintHelper`，是一个约束助手，相对于`Flow`来说，`Layer`的使用较为简单，常用来增加背景，或者共同动画，图层 (`Layer`) 在布局期间会调整大小，其大小会根据其引用的所有视图进行调整

+ 2.7 ImageFilterButton & ImageFilterView

https://medium.com/android-news/constraint-layout-performance-870e5f238100

My point of this example is that layouts which are created to resolve specific cases are better than more general layouts like Constraint Layout