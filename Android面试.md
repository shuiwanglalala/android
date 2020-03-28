# Android面试

+ 页面

  + 布局

    + 布局可定义应用中的界面结构（例如 Activity 的界面结构）。布局中的所有元素均使用 View 和 ViewGroup 对象的层次结构进行构建。View 通常绘制用户可查看并进行交互的内容。然而，ViewGroup 是不可见容器，用于定义 View 和其他 ViewGroup 对象的布局结构

    + 您可通过两种方式声明布局：

      + 在 XML 中声明界面元素
        + 通过在 XML 中声明界面，您可以将应用外观代码与控制其行为的代码分开。使用 XML 文件还有助于为不同屏幕尺寸和屏幕方向提供不同布局
      + 在运行时实例化布局元素

    + 属性

      + 布局参数
        + 名为 layout_something 的 XML 布局属性可以为视图定义适合其所在 ViewGroup 的布局参数。每个 ViewGroup 类都会实现一个扩展 ViewGroup.LayoutParams 的嵌套类。此子类包含的属性类型会根据需要为视图组的每个子视图定义尺寸和位置

    + ConstraintLayout

    + RecyclerView

      + 组成

        - Adapter：为Item提供数据
          - onCreateViewHolder()
          - onBindViewHolder()
          - getItemCount()
        - Layout Manager：Item的布局
        - Item Decoration：Item之间的Divider

      + RecyclerView相比ListView，有一些明显的优点

        + 默认已经实现了View的复用，不需要类似if(convertView == null)的实现，而且回收机制更加完善
        + 默认支持局部刷新

      + 性能优化

        + 数据处理和视图加载分离 spannel

        + ```
          void onItemsInsertedOrRemoved() {
             if (hasFixedSize) layoutChildren();
             else requestLayout();
          }
          ```

        + 如果不要求动画，把默认动画关闭来提升效率

        + 通过 RecycleView.setItemViewCacheSize(size); 来加大 RecyclerView 的缓存，用空间换时间来提高滚动的流畅性

        + 对 ItemView 设置监听器，不要对每个 Item 都调用 addXxListener，应该大家公用一个 XxListener，根据 ID 来进行不同的操作

        + item扁平化

        + 局部刷新

    + 改善布局性能

      + 检测
        + 过度绘制
        + systemtrace查看xml解析
      + 改善的方向和原理
        + 没有特殊需求，选FrameLayout
        + ConstraintLayout
        + include merge
        + ViewStub
          + 当您想要加载 ViewStub 指定的布局时，可通过调用 setVisibility(View.VISIBLE) 将其设为可见，或调用 inflate()

  + View

    + 绘制机制
      + requestLayout()
        + This will trigger onMeasure and onLayout not only for this view but all the way up the line for the parent views
        + Calling requestLayout() is not guaranteed to result in an onDraw (contrary to what the diagram in the accepted answer implies), so it is usually combined with invalidate()
      + invalidate()
        + a redraw of the view
    + 自定义view
      + 类型
        + 完全自定义的组件
        + 复合控件 layout
        + 修改现有 View 类型
      + 实现
        + 至少提供一个以 Context 和 AttributeSet 对象为参数的构造函数
        + 自定义属性 declare-styleable
        + 应用自定义属性 obtainStyledAttributes TypedArray
        + 监听 事件分发
      + 效率
        + 剔除 onDraw() 中的分配，因为分配可能会引起垃圾回收，从而造成卡顿
        + 减少不变要的 invalidate() 调用
        + 尽可能保持较浅的视图层次结构 requestLayout

+ 动画
  + 视图动画 View Animation
    + 补间动画 Tween Animation
      + 平移动画（Translate）
      + 缩放动画（scale）
      + 旋转动画（rotate）
      + 透明度动画（alpha）
      + 实现方式
        + 通过确定开始的视图样式 & 结束的视图样式、中间动画变化过程由系统补全（插值器）来确定一个动画
        + xml
        + java
      + 使用组合动画需要用到标签  Set
      + 监听动画 setAnimationListener
    + 帧动画 
      + 按序播放一组预先定义好的图片 放电影
      + 实现方式
        + xml animation-list
        + java
      + 优点：使用简单、方便
      + 缺点：容易引起 OOM，因为会使用大量 & 尺寸较大的图片资源
  + 属性动画 
    + 在一定时间间隔内，通过不断对值进行改变，并不断将该值赋给对象的属性，从而实现该对象在该属性上的动画效果
    + 逐帧动画 & 补间动画存在一定的缺点
      + 作用对象局限：View
      + 没有改变View的属性，只是改变视觉效果
      + 动画效果单一
    + 优点
      + 作用对象：任意 Java 对象
      + 实现的动画效果：可自定义各种动画效果
    + 做一个属性动画的方式
      + 给你的对象加上get和set方法，前提是你有权限
      + 用一个类来包装原始对象，间接为其提供get和set方法
  + 性能优化
    + 帧动画 图片大小
    + 属性动画 取消repeat的时机
    + 一个view同时发生多种效果时，建议使用PropertyValuesHolder，这样ObjectAnimator只有一个对象
    + 一个view的单个属性先后发生一系列变化时，建议使用Keyframe达到效果
    + 使用ViewPropertyAnimator，简便写法

+ drawable
  + 格式
    + gif 无损 索引色8
    + jpeg 有损  直接色32
    + png-24 无损 直接色
    + svg 无损 矢量
    + .9.png
      + 可拉伸，不可压缩，所以尽可能的小
      + 上边线：图像横向可拉伸的部分
      + 左边线：图像纵向可拉伸的部分
      + 右边线：图像纵向可填充内容（文字或图片）区域
      + 下边线：图像横向可填充内容（文字或图片）区域
  + gilde
    + 使用Glide加载本地图片时最好将磁盘缓存策略设置为NONE，其次避免出现类似国际化资源出现的问题
    + 加载Gif图片时显示奇慢 asGIf(), DiskCacheStrategy.SOURCE/NONE
    + 不要再非主线程里面使用Glide加载图片，如果真的使用了，请把context参数换成getApplicationContext
  + imageview
    + centerCrop centerInside
  + 硬件加速
    + API 级别为 14 及更高级别，则硬件加速默认处于启用状态。并非所有 2D 绘制操作都支持硬件加速，因此启用硬件加速可能会影响您的部分自定义视图或绘制调用
    + 在以下级别控制硬件加速 有可能是失效
      + 应用
      + Activity
      + 窗口
      + 视图
  + 减少过度绘制
    + 检测 开发者选项
    + 方式
      + 移除布局中不需要的背景
      + 使视图层次结构扁平化
      + 降低透明度
        + 例如，要获得灰色文本，您可以在 TextView 中绘制黑色文本，再为其设置半透明的透明度值。但是，您可以简单地通过用灰色绘制文本来获得同样的效果，而且能够大幅提升性能
  + 图片优化
    + memorySize ≈ width * height * 每个像素需要的字节数
    + scale = 设备分辨率 / 资源目录分辨率。同一张图片，放在不同的drawable中，占用的内存大小不同。从公式可看出，使用同一个设备时，drawable表示的分辨率越高，则图片占用的内存越小，反之越大
    + 同样是存放图片的位置，为什么mipmap不在这种情况的考虑范围之内呢？因为mipmap是Android系统为了避免Launcher Icon变形而添加的资源目录，也就是说，mipmap中的图片不会被缩放。所以Google也不推荐将除Launcher Icon之外的图片放在mipmap目录中
    + Bitmap.Config
    + 加载框架设置缓存

+ 音频
  + 音频焦点管理
    + 为了避免所有音乐应用同时播放，Android 引入了“音频焦点”的概念。 一次只能有一个应用获得音频焦点
  + exoplayer audiorecord

+ 后台
  + 服务
    + 绑定服务
      + 如果您的服务已启动并接受绑定，则当系统调用您的 onUnbind() 方法时，如果您想在客户端下一次绑定到服务时接收 onRebind() 调用，则可选择返回 true。onRebind() 返回空值，但客户端仍在其 onServiceConnected() 回调中接收 IBinder
    + AIDL
      + 不应从 Activity 的主线程调用该服务，因为这可能会使应用挂起（Android 可能会显示“Application is Not Responding”对话框）— 通常，您应从客户端内的单独线程调用服务
      + IBinder 方法必须实现为线程安全方法，远程调用时线程是不确定的
+ 进程 线程
  + 进程，是计算机中的程序关于某数据集合上的一次运行活动，是系统进行资源分配和调度的基本单位，是操作系统结构的基础。它的执行需要系统分配资源创建实体之后，才能进行
  + 进程是资源分配的基本单位，线程是调度的基本单位
  + 进程的个体间是完全独立的，而线程间是彼此依存的。多进程环境中，任何一个进程的终止，不会影响到其他进程。而多线程环境中，父线程终止，全部子线程被迫终止(没有了资源)。而任何一个子线程终止一般不会影响其他线程，除非子线程执行了exit()系统调用。任何一个子线程执行exit()，全部线程同时灭亡
  + 多进程环境间完全独立，要实现通信的话就得采用进程间的通信方式，它们通常都是耗时间的。而线程则不用任何手段数据就是共享的。当然多个子线程在同时执行写入操作时需要实现互斥，否则数据就写“脏”了
  + 当应用组件启动且该应用未运行任何其他组件时，Android 系统会使用单个执行线程为应用启动新的 Linux 进程。默认情况下，同一应用的所有组件会在相同的进程和线程（称为“主”线程）中运行。如果某个应用组件启动且该应用已存在进程（因为存在该应用的其他组件），则该组件会在此进程内启动并使用相同的执行线程。但是，您可以安排应用中的其他组件在单独的进程中运行，并为任何进程创建额外的线程
  + android多进程 android:process
    + 作用
      + 分散内存的占用
      + 实现多模块
      + 子进程奔溃，主进程可以继续工作
      + 保活
    + 特点
      + Application的多次重建
      + 静态成员的失效
      +  文件共享问题
        + 多进程的时候不并发访问同一个文件，比如子进程涉及到操作数据库，就可以考虑调用主进程进行数据库的操作
  + 进程级别
    + 前台进程
      + 它正在用户的互动屏幕上运行一个 Activity（其 onResume() 方法已被调用）
      + 它有一个 BroadcastReceiver 目前正在运行（其 BroadcastReceiver.onReceive() 方法正在执行）
      + 它有一个 Service 目前正在执行其某个回调（Service.onCreate()、Service.onStart() 或 Service.onDestroy()）中的代码
    + 可见进程
      + 它正在运行的 Activity 在屏幕上对用户可见，但不在前台（其 onPause() 方法已被调用）。举例来说，如果前台 Activity 显示为一个对话框，而这个对话框允许在其后面看到上一个 Activity，则可能会出现这种情况
      + 它有一个 Service 正在通过 Service.startForeground()
    + 服务进程
      + 包含一个已使用 startService() 方法启动的 Service
      + 已经运行了很长时间（例如 30 分钟或更长时间）的服务的重要性可能会降位，以使其进程降至下文所述的缓存 LRU 列表
    + 缓存进程 LRU
      + 目前不需要的进程，因此，如果其他地方需要内存，系统可以根据需要自由地终止该进程。在正常运行的系统中，这些是内存管理中涉及的唯一进程：运行良好的系统将始终有多个缓存进程可用（为了更高效地切换应用），并根据需要定期终止最早的进程。只有在非常危急（且具有不良影响）的情况下，系统中的所有缓存进程才会被终止，此时系统必须开始终止服务进程
      + 这些进程通常包含用户当前不可见的一个或多个 Activity 实例（onStop() 方法已被调用并返回）
    + 进程的优先级也可能因从属于进程的其他依赖项而提升。例如，如果进程 A 已通过 Context.BIND_AUTO_CREATE 标记绑定到 Service，或在使用进程 B 中的 ContentProvider，则进程 B 的分类始终至少和进程 A 一样重要
  + 跨进程通信
    + 使用文件共享方式，多进程读写一个相同的文件，获取文件内容进行交互
    + 四大组件间传递Bundle
      + 通过 intent 发送数据时，应小心地将数据大小限制为几 KB。发送过多数据会导致系统抛出 TransactionTooLargeException 异常
    + 使用Messenger，一种轻量级的跨进程通讯方案，底层使用AIDL实现
    + 使用AIDL(Android Interface Definition Language)，Android接口定义语言，用于定义跨进程通讯的接口
    + 使用ContentProvider，常用于多进程共享数据，比如系统的相册，音乐等，我们也可以通过ContentProvider访问到
    + 使用Socket传输数据
    + Binder
      + 一次完整的 Binder IPC 通信过程通常是这样

        + 首先 Binder 驱动在内核空间创建一个数据接收缓存区
        + 接着在内核空间开辟一块内核缓存区，建立内核缓存区和内核中数据接收缓存区之间的映射关系，以及内核中数据接收缓存区和接收进程用户空间地址的映射关系
        + 发送方进程通过系统调用 copyfromuser() 将数据 copy 到内核中的内核缓存区，由于内核缓存区和接收进程的用户空间存在内存映射，因此也就相当于把数据发送到了接收进程的用户空间，这样便完成了一次进程间的通信
      + 我们大致能总结出 Binder 通信过程
        + 首先，一个进程使用 BINDERSETCONTEXT_MGR 命令通过 Binder 驱动将自己注册成为 ServiceManager
        + Server 通过驱动向 ServiceManager 中注册 Binder（Server 中的 Binder 实体），表明可以对外提供服务。驱动为这个 Binder 创建位于内核中的实体节点以及 ServiceManager 对实体的引用，将名字以及新建的引用打包传给 ServiceManager，ServiceManger 将其填入查找表
        + Client 通过名字，在 Binder 驱动的帮助下从 ServiceManager 中获取到对 Binder 实体的引用，通过这个引用就能实现和 Server 进程的通信
          + 当 A 进程想要获取 B 进程中的 object 时，驱动并不会真的把 object 返回给 A，而是返回了一个跟 object 看起来一模一样的代理对象 objectProxy，这个 objectProxy 具有和 object 一摸一样的方法，但是这些方法并没有 B 进程中 object 对象那些方法的能力，这些方法只需要把把请求参数交给驱动即可。对于 A 进程来说和直接调用 object 中的方法是一样的。当 Binder 驱动接收到 A 进程的消息后，发现这是个 objectProxy 就去查询自己维护的表单，一查发现这是 B 进程 object 的代理对象。于是就会去通知 B 进程调用 object 的方法，并要求 B 进程把返回结果发给自己。当驱动拿到 B 进程的返回结果后就会转发给 A 进程，一次通信就完成
      + 现在我们可以对 Binder 做个更加全面的定义了
        + 从进程间通信的角度看，Binder 是一种进程间通信的机制
        + 从 Server 进程的角度看，Binder 指的是 Server 中的 Binder 实体对象
        + 从 Client 进程的角度看，Binder 指的是对 Binder 代理对象，是 Binder 实体对象的一个远程代理
        + 从传输过程的角度看，Binder 是一个可以跨进程传输的对象；Binder 驱动会对这个跨越进程边界的对象对一点点特殊处理，自动完成代理对象和本地对象之间的转换
  + 线程
    + 主线程
      + 不要阻塞 UI 线程
        + 将大量或冗长的任务从主线程中移出，使其不影响流畅渲染和快速响应用户输入，这是您在应用中采用线程处理的最大原因
      + 不要在 UI 线程之外访问 Android UI 工具包
        + 我们建议您不要在应用的线程处理工作任务中包含对界面对象的显式引用。避免此类引用有助于防止这些类型的内存泄漏，同时避开线程处理争用
        + 内部类隐式引用外部activity
    + 工作线程
      + 在应用中创建和管理线程时，请务必设置线程的优先级
    + 切线程
      + handler
        + Handler
          + 在未来某个时间点处理 Messages 或者执行 Runnables
          + 将一段逻辑切换到另一个线程执行
          + 构造 Handler 对象的时候如果不传 Looper 参数，会默认使用当前线程关联的 Looper，如果当前线程没有关联 Looper，会抛出异常
        + Looper
          + 用于为线程执行消息循环的类。线程默认没有关联的消息循环，如果要创建一个，可以在执行消息循环的线程里面调用 prepare() 方法，然后调用 loop() 处理消息，直到循环停止
          + 一个线程里调用多次 Looper.prepare() 会抛出异常，提示 Only one Looper may be created per thread，即 一个线程只能创建一个 Looper。Looper 只能关联到一个线程，且关联之后不能改变
        + MessageQueue
          + 持有将被 Looper 分发的消息列表的底层类。消息都是通过与 Looper 关联的 Handler 添加到 MessageQueue，而不是直接操作 MessageQueue
          + Looper 与 MessageQueue 是一一对应的关系
        + Message
          +  消息可以插队，使用 Handler.xxxAtFrontOfQueue 方法
          + 尚未分发的消息是可以撤回的，处理过的就没法了
      + handlerthread
      + intentservice 封装handlerthread
      + AsyncTask
        + 默认情况下，应用会将其创建的所有 AsyncTask 对象推送到单个线程中。因此，它们按顺序执行，而且与主线程一样，特别长的工作数据包可能会阻塞队列。鉴于这个原因，我们建议您仅使用 AsyncTask 处理持续时间短于 5ms 的工作项
        + AsyncTask 可能需要引用某个界面对象，以便 AsyncTask 在主线程上执行其回调后正确更新该界面对象。在这种情况下，您可以使用 WeakReference 存储对所需界面对象的引用
      + ThreadPoolExecutor
      + rxjava

+ 触摸和输入
  + 事件侦听器
    + 硬按键事件总是传递给目前处于焦点的视图对象
    + 请注意不要创建针对 ACTION_DOWN 事件返回 false 的监听器。如果您这样做，系统便无法针对后续一连串 ACTION_MOVE 和 ACTION_UP 事件调用监听器。这是因为 ACTION_DOWN 是所有轻触事件的起点
  + 事件处理程序
    + 不论 View 自身是否注册点击事件，只要 View 是可点击的就会消费事件
      - 上面说的是可点击，可点击包括很多种情况，只要你给View注册了 onClickListener、onLongClickListener、OnContextClickListener 其中的任何一个监听器或者设置了android:clickable=”true” 就代表这个 View 是可点击的。另外，某些 View 默认就是可点击的，例如，Button，CheckBox 等
    + 事件是否被消费由返回值决定，true 表示消费，false 表示不消费，与是否使用了事件无关
    + 所有事件都应该被同一 View 消费
      - 安卓为了保证所有的事件都是被一个 View 消费的，对第一次的事件( ACTION_DOWN )进行了特殊判断，View 只有消费了 ACTION_DOWN 事件，才能接收到后续的事件(可点击控件会默认消费所有事件)，并且会将后续所有事件传递过来，不会再传递给其他 View，除非上层 View 进行了拦截。如果上层 View 拦截了当前正在处理的事件，会收到一个 ACTION_CANCEL，表示当前事件已经结束，后续事件不会再传递过来
  + 手势检测  GestureDetector
    + OnDoubleTapListener

      - onDoubleTap
        - onDoubleTap 在第二次手指按下(down)时触发
      - onSingleTapConfirmed
        - 如果你只想监听双击事件，那么只用关注 onDoubleTap 就行了，如果你同时要监听单击事件则需要关注 onSingleTapConfirmed 这个回调函数
        - 需要同时监听单击和双击，则说明单击和双击后响应逻辑不同，然而使用 OnClickListener 会在双击事件发生时触发两次，这显然不是我们想要的结果。而使用 onSingleTapConfirmed 就不用考虑那么多了，你完全可以把它当成单击事件来看待，而且在双击事件发生时，onSingleTapConfirmed 不会被调用，这样就不会引发冲突
      - onDoubleTapEvent
        - 在双击事件确定发生时会对第二次按下产生的 MotionEvent 信息进行回调
        - onDoubleTapEvent 是一种实时回调

+ 应用数据和文件

  + 

  + |                    | Type of content                                     | Access method                                                | Permissions needed                                           | Can other apps access?                                       | Files removed on app uninstall? | 文件大小       |
    | ------------------ | --------------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------- | -------------- |
    | App-specific files | Files meant for your app's use only                 | From internal storage, `getFilesDir()` or `getCacheDir()`  From external storage, `getExternalFilesDir()` or `getExternalCacheDir()` | Never needed for internal storage  Not needed for external storage when your app is used on devices that run Android 4.4 (API level 19) or higher | No, if files are in a directory within internal storage  Yes, if files are in a directory within external storage | Yes                             | 内部小，外部大 |
    | Media              | Shareable media files (images, audio files, videos) | Environment.getExternalStorageDirectory()                    | `READ_EXTERNAL_STORAGE` or `WRITE_EXTERNAL_STORAGE` when accessing other apps' files on Android 10 (API level 29) or higher  Permissions are required for **all** files on Android 9 (API level 28) or lower | Yes, though the other app needs the `READ_EXTERNAL_STORAGE` permission | No                              | 大             |
    |                    |                                                     |                                                              |                                                              |                                                              |                                 |                |
    | App preferences    | Key-value pairs                                     | [Jetpack Preferences](https://developer.android.com/guide/topics/ui/settings/use-saved-values?hl=zh-cn) library | None                                                         | NO                                                           | Yes                             | 小             |
    | Database           | Structured data                                     | [Room](https://developer.android.com/training/data-storage/room?hl=zh-cn) persistence library | None                                                         | No                                                           | Yes                             | 小             |

    

  + App-specific storage

  + Shared storage

  + Preferences

    + apply() 会立即更改内存中的 SharedPreferences 对象，但会将更新异步写入磁盘。或者，您也可以使用 commit() 将数据同步写入磁盘。但由于 commit() 是同步的，您应避免从主线程调用它，因为它可能会暂停您的界面呈现

  + Databases

    + Entity：表示数据库中的表

    + DAO：包含用于访问数据库的方法

    + 数据库：包含数据库持有者，并作为应用已保留的持久关系型数据的底层连接的主要接入点

      使用 @Database 注释的类应满足以下条件：

      + 是扩展 RoomDatabase 的抽象类
      + 在注释中添加与数据库关联的实体列表
      + 包含具有 0 个参数且返回使用 @Dao 注释的类的抽象方法
        在运行时，您可以通过调用 Room.databaseBuilder() 或 Room.inMemoryDatabaseBuilder() 获取 Database 的实例

      