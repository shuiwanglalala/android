# ViewGroup

[views-widgets-samples](https://github.com/android/views-widgets-samples)



[Android 性能优化（二）之布局优化面面观](https://juejin.im/post/58a442b661ff4b006c8a63f5)

- Avoid Overdraw
- merge标签常用于减少布局嵌套层次，但是只能用于根布局
- App里常见的视图如蒙层、小红点，以及网络错误、没有数据等公共视图，使用频率并不高，如果每一次都参与绘制其实是浪费资源的，都可以借助ViewStub标签进行延迟初始化，仅当使用时才去初始化

