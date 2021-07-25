# [DataBinding最全使用说明](https://juejin.cn/post/6844903549223059463#heading-0)

有很多细节的说明，但不一定正确，需要实践验证，毕竟博客写作的时间比较早

## 布局

**自动布局属性**

但是setter方法只支持单个参数

## 注解

### @BindingAdapter

修饰方法, 要求方法必须`public static`

第一个参数必须是控件或其父类

方法名随意

最后这个`boolean`类型是可选参数. 可以要求是否所有参数都需要填写. 默认true

如果`requireAll`为false, 你没有填写的属性值将为null. 所以需要做非空判断