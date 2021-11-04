# Jetpack新成员Hilt实践

https://github.com/hi-dhl/AndroidX-Jetpack-Practice



https://juejin.cn/post/6844904198803292173#heading-12

**Hilt 如果和 ViewModel 一起使用有点需要注意**

如果使用的是 kotlin 语言的话，需要额外在 App 模块中的 build.gradle 文件中添加以下代码，否则调用 `by viewModels()` 会编译不过

```gradle
kotlinOptions {
    jvmTarget = "1.8"
}
```



https://juejin.cn/post/6845166890562617352#heading-16

对比的部分还挺不错