# Drawables overview

+ 静态图片 Drawable
  + Drawable和View的区别
  + 图层列表 LayerDrawable
    + 转换可绘制对象 TransitionDrawable
  + 形状可绘制对象 GradientDrawable
    + [Padding doesn't affect <shape> in an XML Layout](https://stackoverflow.com/questions/1283085/padding-doesnt-affect-shape-in-an-xml-layout)
    + 大量重复的、简单的背景shape，可考虑代码设置，只新建基本shape.xml
  + ShapeDrawable
  + NinePatchDrawable
    + [.9.png，全面认识“点九图”](https://zhuanlan.zhihu.com/p/29217200)
  + BitmapDrawable
  + DrawableContainer
    + StateListDrawable
      + 大量重复的、简单的背景seletor，可考虑代码设置
    + LevelListDrawable
  + InsetDrawable
    + 控件范围大于drawable
  + ClipDrawable
    + 默认级别为 0，即完全裁剪，使图像不可见。当级别为 10,000 时，图像不会裁剪，而是完全可见
  + ScaleDrawable
  + VectorDrawable
  + AnimatedVectorDrawable
+ 动画
+ 视频
+ 文字

## Create drawables from resource images

[What are the different usecases of PNG vs. GIF vs. JPEG vs. SVG?](https://stackoverflow.com/questions/2336522/what-are-the-different-usecases-of-png-vs-gif-vs-jpeg-vs-svg)

[Android bitmap(二) 常见图片格式JPG PNG](https://www.jianshu.com/p/371028436de7)

## Create drawables from XML resources

## Custom drawables

*CircularProgressDrawable*

*RoundedDrawable*

