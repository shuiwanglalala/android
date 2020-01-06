# Application

[Understanding the Android Application Class](https://github.com/codepath/android_guides/wiki/Understanding-the-Android-Application-Class)

you should never store mutable shared data inside the Application object since that data might disappear or become invalid at any time

Bottom Line: Storing data in the Application object is error-prone and can crash your app. Prefer storing your global data on disk if it is really needed later or explicitly pass to your activity in the intent’s extras

------

[Android：全面解析 Application类](https://juejin.im/entry/59c30e0ff265da06611f7024)

------

+ 全局性初始化
+ 获取application context
+ 注册监听
  + [ActivityLifecycleCallbacks](https://droidyue.com/blog/2016/02/21/thinking-of-getting-the-current-activity-in-android/)
  + ComponentCallbacks2