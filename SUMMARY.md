# Summary

* [Introduction](README.md)
* [应用权限](应用权限.md)
  * [Permissions overview](Permissions overview.md)
  * [在运行时请求权限](在运行时请求权限.md)
* Activities
  * [Introduction to Activities](Introduction to Activities.md)
  * [Understand the Activity Lifecycle](Understand the Activity Lifecycle.md)
  * [Tasks and Back Stack](Tasks and Back Stack.md)
  * [Parcelables and Bundles](Parcelables and Bundles.md)
  * [Fragments](Fragments.md)
    * 构建灵活的界面
    * 与其他 Fragment 通信
    * [Fragments的弊端](Fragments的弊端.md)
  * [Application](Application.md)
  * [Window](Window.md)
* Architecture Components
  * [数据绑定库](数据绑定库.md)
  * [Handling Lifecycles with Lifecycle-Aware Components](Handling Lifecycles with Lifecycle-Aware Components.md)
  * [LiveData](LiveData.md)
  * [Paging library](Paging library.md)
    * [Paging library overview](Paging library overview.md)
    * [Display paged lists](Display paged lists.md)
    * [Gather paged data](Gather paged data.md)
  * [Room Persistence Library](Room Persistence Library.md)
  * [ViewModel](ViewModel.md)
  * [WorkManager](WorkManager.md)
    * 方法指南
      * [Defining your Work Requests](Defining your Work Requests.md)
      * [工作状态和观察工作](工作状态和观察工作.md)
      * [链接工作](链接工作.md)
      * [Cancelling and stopping work](Cancelling and stopping work.md)
    * 高级概念
      * 在WorkManager中进行线程处理
        * [Threading in Worker](Threading in Worker.md)
  * [Saving UI States](Saving UI States.md)
  * [architectural tools and patterns](architectural tools and patterns.md)
    * [mvp](mvp.md)
    * [mvp-clean](mvp-clean.md)
    * [mvp-dagger](mvp-dagger.md)
    * [mvp-rxjava](mvp-rxjava.md)
    * [todo-mvvm-databinding](todo-mvvm-databinding.md)
* User interface
  * Layouts
    * Create a List with RecyclerView
      * [RecyclerView](RecyclerView.md)
  * [Dialogs](Dialogs.md)
    * [自定义Dialog](自定义Dialog.md)
  * [View](View.md)
    * 机制
      * [绘制](绘制.md)
      * 滚动
      * [事件分发](事件分发.md)
    * 实例
      * [ViewGroup](ViewGroup.md)
        * [ConstraintLayout](ConstraintLayout.md)
          * MotionLayout
        * DrawerLayout
        * [SwipeRefreshLayout](SwipeRefreshLayout.md)
        * FrameLayout
          * [CardView](CardView.md)
      * View
        * [Snackbar-Toast](Snackbar-Toast.md)
        * [TextView](TextView.md)
        * ProgressBar
          * [SeekBar](SeekBar.md)
      * 自定义view
        * [Creating a View Class](Creating a View Class.md)
        * [Optimizing the View](Optimizing the View.md)
* 图片和图形
  * [Drawables overview](Drawables overview.md)
  * [Vector drawables overview](Vector drawables overview.md)
  * [Handling bitmaps](Handling bitmaps.md)
  * [Hardware acceleration](Hardware acceleration.md)
* 音频和视频
  * [MediaPlayer 概览](MediaPlayer 概览.md)
  * [MediaRecorder overview](MediaRecorder overview.md)
* [Background Tasks](Background Tasks.md)
  * [服务](服务.md)
    * [绑定服务](绑定服务.md)
    * [Android 接口定义语言](Android 接口定义语言.md)
  * [Broadcasts overview](Broadcasts overview.md)
  * Manage device awake state
    * [使设备保持唤醒状态](使设备保持唤醒状态.md)
  * [Jobscheduler](Jobscheduler.md)
* [App data & files](App data & files.md)
  - [Save files on device storage](Save files on device storage.md)
  - [Save key-value data](Save key-value data.md)
  - [Save data in a local database](Save data in a local database.md)
    - 将数据保存到本地数据库
      - [Defining data using Room entities](Defining data using Room entities.md)
      - 使用DAO访问数据
    - nosql
      - [SnappyDB](SnappyDB.md)
    - orm
      - [Ormlite](Ormlite.md)
+ [Touch and input](Touch and input.md)
  + Using touch gestures
    + [Detect common gestures](Detect common gestures.md)
    + [Track touch and pointer movements](Track touch and pointer movements.md)
    + [处理多点触控手势](处理多点触控手势.md)
    + [拖动和缩放](拖动和缩放.md)
    + [Manage touch events in a ViewGroup](Manage touch events in a ViewGroup.md)
  + Handling keyboard input
    + [Specify the input method type](Specify the input method type.md)
    + [Handle input method visibility](Handle input method visibility.md)
+ Performance
  + Android vitals
    + [ANRs](ANRs.md)
    + [App startup time](App startup time.md)
  + [进程和线程](进程和线程.md)
  + [Better performance through threading](Better performance through threading.md)
    + [Handler](Handler.md)
  + 针对电池续航时间进行优化
    + [针对低电耗模式和应用待机模式进行优化](针对低电耗模式和应用待机模式进行优化.md)
  + [Manage your app memory](Manage your app memory.md)
    + [内存泄漏](内存泄漏.md)
  + [使应用能迅速响应](使应用能迅速响应.md)
  + [性能提示](性能提示.md)
+ 其他
  + [PackageManager](PackageManager.md)
+ 编写您的应用
  + [利用注解改进代码检查](利用注解改进代码检查.md)
+ Debug your app
  + [使用布局检查器调试您的布局](使用布局检查器调试您的布局.md)
+ Profile your app
  + Inspect device activity with Systrace
  + Inspect CPU activity
    + [Inspect trace logs with Traceview](Inspect trace logs with Traceview.md)
  + 使用 Memory Profiler 查看 Java 堆和内存分配
    + [调查 RAM 使用情况](调查 RAM 使用情况.md)
+ 库
  + [响应式](响应式.md)
    + [ReactiveX](ReactiveX.md)
    + Awesome-RxJava
    + Rxjava
      + [Rxjava 1.0](Rxjava 1.0.md)
      + [Rxjava 2.0](Rxjava 2.0.md)
    + [Rxbinding](Rxbinding.md)
    + RxLifecycle
  + [Retrofit](Retrofit.md)
  + [Util](Util.md)
    + [Guava](Guava.md)
+ 开始
  + [基本语法](基本语法.md)
+ 类和对象
  + [属性和字段](属性和字段.md)
  + [泛型](泛型.md)
  + [委托属性](委托属性.md)
+ 函数和Lamdba表达式
  + [内联函数](内联函数.md)
+ [协程](协程.md)
+ 注解
  - [注解](注解.md)
  - 编写注解处理器
    - 默认值限制
+ Java 8
  + [lambda](lambda.md)
+ [语法与数据类型](语法与数据类型.md)
+ [流程控制与错误处理](流程控制与错误处理.md)
+ [循环与迭代](循环与迭代.md)
+ [函数](函数.md)
+ [表达式和运算符](表达式和运算符.md)
+ 
+ [问题](问题.md)