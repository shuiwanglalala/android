# ConstraintLayout

[约束布局ConstraintLayout看这一篇就够了](https://juejin.im/post/5bac92f2f265da0aba70c1bf)

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