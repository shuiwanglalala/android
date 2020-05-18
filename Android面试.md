# Android

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
    + 服务的整个生命周期从调用 onCreate() 开始起，到 onDestroy() 返回时结束
    + 服务的有效生命周期
      - 对于启动服务，从调用 onStartCommand()开始起，到 onDestroy() 返回时结束
      - 对于绑定服务，从调用 onBind()开始起，到 onUnbind() 返回时结束
    + 启动服务
      + 为确保应用的安全性，在启动 Service 时，请始终使用显式 Intent，且不要为服务声明 Intent 过滤器。使用隐式 Intent 启动服务存在安全隐患，因为您无法确定哪些服务会响应 Intent，而用户也无法看到哪些服务已启动
      + startService() 方法将立即返回，且 Android 系统调用服务的 onStartCommand() 方法。如果服务尚未运行，则系统会先调用 onCreate()，然后再调用 onStartCommand()
      + 多个服务启动请求会导致多次对服务的 onStartCommand() 进行相应的调用。但是，要停止服务，只需一个服务停止请求（使用 stopSelf() 或 stopService()）即可
      + START_NOT_STICKY
        如果系统在 onStartCommand() 返回后终止服务，则除非有待传递的挂起 Intent，否则系统不会重建服务
      + START_STICKY
        如果系统在 onStartCommand() 返回后终止服务，则其会重建服务并调用onStartCommand()，但不会重新传递最后一个 Intent。相反，除非有挂起 Intent 要启动服务，否则系统会调用包含空 Intent 的 onStartCommand()。在此情况下，系统会传递这些 Intent。此常量适用于不执行命令、但无限期运行并等待作业的媒体播放器（或类似服务）
      +  START_REDELIVER_INTENT
    + 绑定服务
      + 如果您的服务已启动并接受绑定，则当系统调用您的 onUnbind() 方法时，如果您想在客户端下一次绑定到服务时接收 onRebind() 调用，则可选择返回 true。onRebind() 返回空值，但客户端仍在其 onServiceConnected() 回调中接收 IBinder
    + AIDL
      + 不应从 Activity 的主线程调用该服务，因为这可能会使应用挂起（Android 可能会显示“Application is Not Responding”对话框）— 通常，您应从客户端内的单独线程调用服务
      + IBinder 方法必须实现为线程安全方法，远程调用时线程是不确定的
    + 怎么在Service中创建Dialog对话框
      + 在我们取得Dialog对象后，需给它设置类型，即：
        dialog.getWindow().setType(WindowManager.LayoutParams.TYPE_SYSTEM_ALERT)
      + 在Manifest中加上权限:
        uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" 

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
        + 非UI线程可以更新UI吗?
          + 当访问UI时，ViewRootImpl会调用checkThread方法去检查当前访问UI的线程是哪个，如果不是UI线程则会抛出异常。执行onCreate方法的那个时候ViewRootImpl还没创建，无法去检查当前线程。ViewRootImpl的创建在onResume方法回调之后
          + 非UI线程是可以刷新UI的呀，前提是它要拥有自己的ViewRoot。如果想直接创建ViewRoot实例，你会发现找不到这个类。那怎么做呢？通过WindowManager
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

  + 缓存

    + LruCache
      + A cache that holds strong references to a limited number of values. Each time a value is accessed, it is moved to the head of a queue. When a value is added to a full cache, the value at the end of that queue is evicted and may become eligible for garbage collection
      + By default, the cache size is measured in the number of entries. Override sizeOf(K, V) to size the cache in different units
      + This class is thread-safe
      + key 和 value 不接受 null

+ 内容提供器

  + 通过配置内容提供程序，您可以使其他应用安全地访问和修改您的应用数据
  + Android 框架内的某些内容提供程序可管理音频、视频、图像和个人联系信息等数据。android.provider 软件包参考文档中列出了其中的部分提供程序。虽然存在一些限制，但任何 Android 应用均可访问这些提供程序
  + 内容提供程序以一个或多个表的形式将数据呈现给外部应用，这些表与在关系型数据库中找到的表类似。行表示提供程序收集的某种数据类型实例，行中的每个列表示为实例所收集的每条数据
  + 如要访问内容提供程序中的数据，您可以客户端的形式使用应用的 Context 中的 ContentResolver 对象，从而与提供程序进行通信。ContentResolver 对象会与提供程序对象（即实现 ContentProvider 的类实例）进行通信
  + 内容 URI 包括整个提供程序的符号名称（其授权）和指向表的名称（路径）

+ 广播
  + 一般来说，广播可作为跨应用和普通用户流之外的消息传递系统。但是，您必须小心，不要滥用在后台响应广播和运行作业的机会，因为这会导致系统变慢
  + 此对象仅在调用 onReceive(Context, Intent) 期间有效。一旦从此方法返回代码，系统便会认为该组件不再活跃
    + 您不应从广播接收器启动长时间运行的后台线程。onReceive() 完成后，系统可以随时终止进程来回收内存，在此过程中，也会终止进程中运行的派生线程。要避免这种情况，您应该调用 goAsync()（如果您希望在后台线程中多花一点时间来处理广播）或者使用 JobScheduler
  + 接收广播
    + 清单声明的接收器
      + 如果您在清单中声明广播接收器，系统会在广播发出后启动您的应用（如果应用尚未运行）
      + 如果您的应用以 API 级别 26 或更高级别的平台版本为目标，则不能使用清单为隐式广播（没有明确针对您的应用的广播）声明接收器，但一些不受此限制的隐式广播除外
    + 上下文注册的接收器
      + 只要注册上下文有效，上下文注册的接收器就会接收广播。例如，如果您在 Activity 上下文中注册，只要 Activity 没有被销毁，您就会收到广播。如果您在应用上下文中注册，只要应用在运行，您就会收到广播
      + 当您不再需要接收器或上下文不再有效时，请务必注销接收器
  + 发送广播
    + sendOrderedBroadcast(Intent, String) 方法一次向一个接收器发送广播。当接收器逐个顺序执行时，接收器可以向下传递结果，也可以完全中止广播，使其不再传递给其他接收器。接收器的运行顺序可以通过匹配的 intent-filter 的 android:priority 属性来控制；具有相同优先级的接收器将按随机顺序运行
    + sendBroadcast(Intent) 方法会按随机的顺序向所有接收器发送广播。这称为常规广播。这种方法效率更高，但也意味着接收器无法从其他接收器读取结果，无法传递从广播中收到的数据，也无法中止广播
    + LocalBroadcastManager.sendBroadcast 方法会将广播发送给与发送器位于同一应用中的接收器。如果您不需要跨应用发送广播，请使用本地广播。这种实现方法的效率更高（无需进行进程间通信），而且您无需担心其他应用在收发您的广播时带来的任何安全问题
  + 权限
    + 不是谁都能收到我发的广播 收件人设置
    + 我不接收垃圾短信
  + 安全注意事项和最佳做法
    + 请优先使用上下文注册而不是清单声明
    + 请勿从广播接收器启动 Activity，否则会影响用户体验，尤其是有多个接收器
    + 如果您不需要向应用以外的组件发送广播，则可以使用支持库中提供的 LocalBroadcastManager 来收发本地广播。LocalBroadcastManager 效率更高（无需进行进程间通信），并且您无需考虑其他应用在收发您的广播时带来的任何安全问题。本地广播可在您的应用中作为通用的发布/订阅事件总线，而不会产生任何系统级广播开销
    + 请勿使用隐式 intent 广播敏感信息。任何注册接收广播的应用都可以读取这些信息
    + 广播操作的命名空间是全局性的。请确保在您自己的命名空间中编写操作名称和其他字符串

+ activity
  + 定义
    + 当一个应用调用另一个应用时，调用方应用会调用另一个应用中的 Activity，而不是整个应用。通过这种方式，Activity 充当了应用与用户互动的入口点
  + 生命周期
    + 无论您选择在哪个构建事件中执行初始化操作，都请务必使用相应的生命周期事件来释放资源
    + 横竖屏切换时Activity的生命周期变化
      + 如果自己没有配置android:ConfigChanges，这时默认让系统处理，就会重建Activity，此时Activity的生命周期会走一遍
      + 如果设置  android:configChanges="orientation|keyboardHidden|screenSize">，此时Activity的生命周期不会重走一遍，Activity不会重建，只会回调onConfigurationChanged方法

  + 保持状态
    + 系统永远不会直接终止 Activity 以释放内存，而是会终止 Activity 所在的进程。系统不仅会销毁 Activity，还会销毁在该进程中运行的所有其他内容
    + ViewModel 非常适合在用户正活跃地使用应用时存储和管理界面相关数据。它支持快速访问界面数据，并且有助于避免在发生旋转、窗口大小调整和其他常见的配置更改后从网络或磁盘中重新获取数据
    + 已保存实例状态捆绑包在配置更改和进程终止后都会保留，但受限于存储容量和速度，因为 onSavedInstanceState() 会将数据序列化到磁盘
    + 对复杂或大型数据使用本地持久性存储来处理进程终止
  + 跳转
    + startActivity()
    + startActivityForResult()
    + 从Activity中启动新的Activity时可以直接mContext.startActivity(intent)就好
    + 如果从其他Context中启动Activity则必须给intent设置Flag FLAG_ACTIVITY_NEW_TASK
  + 任务和返回栈
    + 任务是用户在执行某项工作时与之互动的一系列 Activity 的集合。这些 Activity 按照每个 Activity 打开的顺序排列在一个返回堆栈中
    + 使用清单文件
      + standard
      + singleTop
      + singleTask
        + 虽然 Activity 在新任务中启动，但用户按返回按钮仍会返回到上一个 Activity
      + singleInstance
    + 使用 Intent 标记
    + 亲和性
      + When the intent that launches an activity contains the FLAG_ACTIVITY_NEW_TASK flag
      + When an activity has its allowTaskReparenting attribute set to "true"

+ fragment
  + 您可以将片段视为 Activity 的模块化组成部分，它具有自己的生命周期，能接收自己的输入事件，并且您可以在 Activity 运行时添加或移除片段（这有点像可以在不同 Activity 中重复使用的“子 Activity”）
  + 片段必须始终托管在 Activity 中，其生命周期直接受宿主 Activity 生命周期的影响
    + When auto-created, an activity also auto creates and attaches all added fragments
    + The member variables of activities and fragments are NOT restored after they are auto-created
  + 向 Activity 添加片段
    + 在 Activity 的布局文件内声明片段
    + 如要在您的 Activity 中执行片段事务（如添加、移除或替换片段），则必须使用 FragmentTransaction 中的 API
  + 事务管理
    + 在调用 commit() 之前，您可能希望调用 addToBackStack()，以将事务添加到片段事务返回栈。该返回栈由 Activity 管理，允许用户通过按返回按钮返回上一片段状态
    + 向 FragmentTransaction 添加更改的顺序无关紧要，不过
      + 您必须最后调用 commit()，异步的
        + 如有必要，您也可以从界面线程调用 executePendingTransactions()，以立即执行 commit() 提交的事务。通常不必这样做，除非其他线程中的作业依赖该事务
      + 如果您要向同一容器添加多个片段，则您添加片段的顺序将决定它们在视图层次结构中出现的顺序
      + 您只能在 Activity 保存其状态（当用户离开 Activity）之前使用 commit() 提交事务。如果您试图在该时间点后提交，则会引发异常。这是因为如需恢复 Activity，则提交后的状态可能会丢失。对于丢失提交无关紧要的情况，请使用 commitAllowingStateLoss()
  + 注意事项
    + 你在pop了Fragment之后，该Fragment的异步任务仍然在执行，并且在执行完成后调用了getActivity()方法，这样就会空指针
    + 高耦合
      + 通过接口抽象的方法，通过接口去调用宿主Activity的方法
    + 由于采用创建对象的方式去初始化Fragment对象，当宿主Activity在界面销毁或者界面重新执行onCreate()方法时,就有可能再一次的执行Fragment的创建初始，而之前已经存在的 Fragment 实例也会销毁再次创建，这不就与 Activity 中 onCreate() 方法里面第二次创建的 Fragment 同时显示从而发生 UI 重叠的问题
      + 利用savedInstanceState判断

+ Window

  + 应用窗口 1-99 activity dialog
  + 子窗口 1000-1999 popupwindow 
    + 所以称为子窗口，即它的父窗口显示时，子窗口才显示。父窗口不显示，它也不显示。追随父窗口
  + 系统窗口 2000-2999 toast
  + 层级大的会覆盖在层级小的Window上面

+ 视图绑定

  + 与使用 findViewById 相比，视图绑定具有一些很显著的优点
    + Null 安全：由于视图绑定会创建对视图的直接引用，因此不存在因视图 ID 无效而引发 Null 指针异常的风险。此外，如果视图仅出现在布局的某些配置中，则绑定类中包含其引用的字段会使用 @Nullable 标记
    + 类型安全
  + 与数据绑定比较
    + 数据绑定库仅处理使用  layout 代码创建的数据绑定布局
    + 视图绑定不支持布局变量或布局表达式，因此它不能用于在 XML 中将布局与数据绑定

+ 数据绑定库
  + 您可以使用声明性格式（而非程序化地）将布局中的界面组件绑定到应用中的数据源
  + 数据绑定布局文件略有不同，以根标记 layout 开头，后跟 data 元素和 view 根元素

+ Lifecycle
  + 引入
    + 在真实的应用中，最终会有太多管理界面和其他组件的调用，以响应生命周期的当前状态。管理多个组件会在生命周期方法（如 onStart() 和 onStop()）中放置大量的代码，这使得它们难以维护
    + 无法保证组件会在 Activity 或 Fragment 停止之前启动。在我们需要执行长时间运行的操作（如 onStart() 中的某种配置检查）时尤其如此。这可能会导致出现一种竞争条件，在这种条件下，onStop() 方法会在 onStart() 之前结束，这使得组件留存的时间比所需的时间要长

+ livedata

  + 常规的可观察类不同，LiveData 具有生命周期感知能力，意指它遵循其他应用组件（如 Activity、Fragment 或 Service）的生命周期。这种感知能力可确保 LiveData 仅更新处于活跃生命周期状态的应用组件观察者

+ paging

+ viewmodel
  + 引入的缘由
    + 如果系统销毁或重新创建界面控制器，则存储在其中的任何临时性界面相关数据都会丢失。对于简单的数据，Activity 可以使用 onSaveInstanceState() 方法从 onCreate() 中的捆绑包恢复其数据，但此方法仅适合可以序列化再反序列化的少量数据，而不适合数量可能较大的数据
    + 界面控制器经常需要进行异步调用，这些调用可能需要一些时间才能返回结果。界面控制器需要管理这些调用，并确保系统在其销毁后清理这些调用以避免潜在的内存泄露。此项管理需要大量的维护工作，并且在因配置更改而重新创建对象的情况下，会造成资源的浪费，因为对象可能需要重新发出已经发出过的调用
  + 架构组件为界面控制器提供了 ViewModel 辅助程序类，该类负责为界面准备数据。 在配置更改期间会自动保留 ViewModel 对象，以便它们存储的数据立即可供下一个 Activity 或 Fragment 实例使用
    + setRetainInstance(true) 底层实现
  + 生命周期
    + ViewModel 对象存在的时间范围是获取 ViewModel 时传递给 ViewModelProvider 的 Lifecycle。ViewModel 将一直留在内存中，直到限定其存在时间范围的 Lifecycle 永久消失：对于 Activity，是在 Activity 完成时；而对于 Fragment，是在 Fragment 分离时
  + 在 Fragment 之间共享数据

+ WorkManager

  + 可延迟运行（即不需要立即运行）并且在应用退出或设备重启时必须能够可靠运行的任务

+ ANR

  + 触发

    + 当您的 Activity 位于前台时，您的应用在 5 秒钟内未响应输入事件或BroadcastReceiver（如按键或屏幕轻触事件）

    + 虽然前台没有 Activity，但您的 BroadcastReceiver 用了10 秒的时间仍未执行完毕 

    + BroadcastQueue Timeout ：前台广播在10s内、后台广播在20秒内未执行完成；

      Service Timeout ：前台服务在20s内、后台服务在200秒内未执行完成；

      ContentProvider Timeout ：内容提供者,在publish过超时10s

  + 原因

    + 应用在主线程上非常缓慢地执行涉及 I/O 的操作
    + 应用在主线程上进行长时间的计算
    + 主线程在对另一个进程进行同步 binder 调用，而后者需要很长时间才能返回
    + 主线程处于阻塞状态，为发生在另一个线程上的长操作等待同步的块
    + 主线程在进程中或通过 binder 调用与另一个线程之间发生死锁。主线程不只是在等待长操作执行完毕，而且处于死锁状态
    + 其他进程的CPU占用率高，使得当前应用进程无法抢占到CPU时间片

  + 诊断

    + traceview
    + /data/anr/trace文件

  + 修复方式

    + 切线程执行耗时操作 IO 计算
    + 如果某工作线程持有对某项资源的锁，而该资源是主线程完成其工作所必需的，这种情况下就可能会发生 ANR
      + 注意检测锁
    + 广播anr
      + 以下情况下会发生 ANR
        + 广播接收器用了相当长的时间仍未执行完 onReceive()
        + 广播接收器对 PendingResult 对象调用了 goAsync()，但未能调用 finish()
      + 我们建议将长时间运行的操作移至 IntentService

+ 崩溃

  + 触发
    + 使用 Java 编写的应用会在抛出未处理的异常（由 Throwable 类表示）时崩溃。使用原生代码语言编写的应用，会在执行过程中遇到未处理的信号（如 SIGSEGV）时崩溃
  + 检测
    + bugly
    + logcat

+ 呈现速度缓慢

  + 检测
    + 目视检查方法
      + 启用 GPU 呈现模式分析功能。GPU 呈现模式分析功能会在屏幕上显示一些条形，以相对于每帧 16ms 的基准，快速直观地显示呈现界面窗口帧所花的时间
      + 某些组件（如 RecyclerView）是卡顿的常见来源。如果您的应用使用了这些组件，您最好查看一下应用的这些部分
      + 您可以尝试在速度较慢的设备上运行您的应用，以突显此问题
    + Systrace
  + 常见的卡顿来源
    + RecyclerView：notifyDataSetChanged
    + 嵌套 RecyclerView 很常见，对于由水平滚动列表组成的纵向列表（例如 Play 商店主页面上的应用网格），尤其如此。这种方法效果很好，但它也会导致大量来回移动的视图。在首次向下滚动页面时，如果您看到大量内部内容出现扩充，则可能需要检查内部（水平）RecyclerView 之间是否正在共享 RecyclerView.RecycledViewPool
    + 布局性能，改约束布局
    + 一般来说，动画应以 View 的绘制属性（例如 setTranslationX/Y/Z()、setRotation()、setAlpha() 等等）运行。与布局属性（例如，内边距或外边距）相比，这些属性的更改开销要低得多
    + 一般来说，解决方法是避免调用进行 binder 调用的函数；如果不可避免，则应该缓存相应值，或将工作转移到后台线程
    + 请记住，每次分配都会产生开销。如果它处于被频繁调用的紧密循环中，请考虑避免分配以减轻 GC 上的负载

+ 应用启动时间

  + 冷启动 系统进程在冷启动后才创建应用进程
  + 热启动 在热启动中，系统的所有工作就是将您的 Activity 带到前台。如果应用的所有 Activity 都还驻留在内存中，则应用可以无须重复对象初始化、布局扩充和呈现
  + 温启动
    + 系统将您的应用从内存中逐出，然后用户又重新启动它。进程和 Activity 需要重启，但传递到 onCreate() 的已保存实例状态包对于完成此任务有一定助益
  + 诊断
    +  ActivityManager: Displayed com.android.myexample/.StartupTiming: +3s534ms
    + traceview
  + 修复
    + 解决方案都需要延迟初始化对象：仅初始化立即需要的对象
    + 此外，考虑使用依赖注入框架（如 Dagger），它们会在首次注入时创建对象和依赖项
    + 通过减少冗余或嵌套布局，展平您的视图层次结构
    + 不要扩充在启动期间无需显示的界面部分。而是使用 ViewStub
    + application设置windowBackground，避免长时间黑屏

+ 减小apk大小

  + 移除未使用的资源
  + 要仅包含您的应用所需的库部分，您可以编辑库的文件（如果库许可允许您修改库）
  + 仅支持特定密度
  + 使用可绘制对象 矢量图
  + 压缩png
  + 移除不必要的生成代码
  + 避免使用枚举

+ 内存

  + 指标

    + USS	Unique Set Size	物理内存	进程独占的内存
      PSS	Proportional Set Size	物理内存	PSS= USS+ 按比例包含共享库
      RSS	Resident Set Size	物理内存	RSS= USS+ 包含共享库
      VSS	Virtual Set Size	虚拟内存	VSS= RSS+ 未分配实际物理内存

  + 检测内存使用情况

    + Android Monitor
    + 捕捉堆转储
      + 堆转储是应用堆中所有对象的快照。堆转储以一种名称为 HPROF 的二进制格式存储
      + 要分析堆转储，您可以使用标准工具，如 jhat。要使用 jhat，您需要将 HPROF 文件从 Android 格式转换为 Java SE HPROF 格式。要转换为 Java SE HPROF 格式

  + 垃圾回收

    + Android 的内存堆是分代的，这意味着它会根据分配对象的预期寿命和大小跟踪不同的分配存储分区。例如，最近分配的对象属于“新生代”。当某个对象保持活动状态达足够长的时间时，可将其提升为较老代，然后是永久代

      堆的每一代对相应对象可占用的内存量都有其自身的专用上限。每当一代开始填满时，系统便会执行垃圾回收事件以释放内存。垃圾回收的持续时间取决于它回收的是哪一代对象以及每一代有多少个活动对象

      尽管垃圾回收速度非常快，但仍会影响应用的性能。通常情况下，您无法从代码中控制何时发生垃圾回收事件。系统有一套专门确定何时执行垃圾回收的标准。当条件满足时，系统会停止执行进程并开始垃圾回收

  + 共享内存

    + 为了在 RAM 中容纳所需的一切，Android 会尝试跨进程共享 RAM 页面

  + 使用内存效率更高的代码结构

    + 谨慎使用服务
    + 使用经过优化的数据容器
      + Android 框架包含几个经过优化的数据容器，包括 SparseArray、SparseBooleanArray 和 LongSparseArray
    + 避免内存抖动
      + 您可以在 for 循环中分配多个临时对象。或者，您也可以在视图的 onDraw() 函数中创建新的 Paint 或 Bitmap 对象。在这两种情况下，应用都会快速创建大量对象。这些操作可以快速消耗新生代 (young generation) 区域中的所有可用内存，从而迫使垃圾回收事件发生

+ 保活

  + 黑色保活：不同的app进程，用广播相互唤醒（包括利用系统提供的广播进行唤醒）
  + 白色保活：启动前台Service

