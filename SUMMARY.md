# Summary

* [Todo](Todo.md)

* software
  
  * 编写您的应用
    
    + 添加多密度矢量图形
    
    + 使用 lint 检查改进您的代码
    
    + 工具属性参考文档
  
  * 构建和运行您的应用
    
    * 概览
    
    * 创建和修改运行/调试配置
  
  * 配置编译版本
    
    * [概览](配置build.md)
    
    * 配置应用模块
    
    * 添加构建依赖项
    
    * 配置 build 变体
    
    * Gradle 提示与诀窍
    
    * 将构建配置从 Groovy 迁移到 KTS
    
    * 优化构建速度
      
      * 概览
    
    * [压缩您的应用](压缩您的应用.md)
    
    * 为方法数超过 64K 的应用启用 MultiDex
  
  * 调试应用
    
    * 使用 Logcat 写入和查看日志
    
    * 使用布局检查器和布局验证工具调试布局
    
    * 使用 Network Inspector 检查网络流量
    
    * 使用 Database Inspector 调试数据库
    
    * 使用 APK 分析器分析您的 build
    
    * [调查 RAM 使用情况](调查RAM使用情况.md)
  
  * 测试应用
    
    * 其他测试工具
      
      * Monkey Testing
  
  * 发布应用
    
    * [为应用签名](为应用签名.md)
  
  * 命令行工具
    
    * Android SDK 构建工具
      
      * aapt2
      
      * d8
    
    * Android SDK 平台工具
      
      * [adb](adb.md)
      
      * dumpsys

* 设备兼容性
  
  * [支持不同的像素密度](支持不同的像素密度.md)

* 应用架构指南
  
  * 页面层
    
    * [界面层概览](界面层概览.md)
    
    * [页面事件](页面事件.md)
  
  * [网域层](网域层.md)
  
  * [数据层](数据层.md)

* 架构组件
  
  * 页面层库
    
    * 生命周期感知型组件
      
      * [处理生命周期](处理生命周期.md)
      
      * [ViewModel](ViewModel.md)
      
      * [LiveData](LiveData.md)
      
      * [将 Kotlin 协程与生命周期感知型组件一起使用](将Kotlin协程与生命周期感知型组件一起使用.md)
  
  * 数据层库
    
    * [DataStore](DataStore.md)

* 应用入口点
  
  * [Activity](Activity.md)
    
    * [Activity生命周期](Activity生命周期.md)
    
    * [任务和返回栈](任务和返回栈.md)
    
    * 从后台启动 Activity 的限制

* [依赖项注入](依赖项注入.md)
  
  * [使用Hilt实现依赖项注入](使用Hilt实现依赖项注入.md)

* Activities
  
  * 与其他应用互动
    * [获取 Activity 的结果](获取Activity的结果.md)
    * [允许其他应用启动您的 Activity](允许其他应用启动您的Activity.md)

* [Fragment](Fragment.md)

* 

* Intent和Intent过滤器
  
  * [Intent概览](Intent概览.md)
  
  * 通信
    
    * [事件总线](事件总线.md)
    
    * [ARouter](ARouter.md)

* [界面](界面.md)
  
  * [Material design](MaterialDesign.md)
    * [ProgressBar](ProgressBar.md)
    * [CardView](CardView.md)
    * [Tablayout](Tablayout.md)
    * [DatePicker](DatePicker.md)
    * [TopAppbar](TopAppbar.md)
  * [View](View.md)
    * [Table](Table.md)
    * [绘制](绘制.md)
      * [HenCoder Android 开发进阶: 自定义 View](HenCoderAndroid开发进阶自定义View.md)
    * [焦点Focus](焦点Focus.md)
  * 布局
    * [ConstraintLayout](ConstraintLayout.md)
    * [RecyclerView](RecyclerView.md)
      * [RecyclerView缓存机制](RecyclerView缓存机制.md)
    * [FlexboxLayout](FlexboxLayout.md)
    * FrameLayout
      * [ScrollView](ScrollView.md)
      * [NestedScrollView](NestedScrollView.md)
    * [ViewPager](ViewPager.md)
    * [SwipeRefreshLayout](SwipeRefreshLayout.md)
  * 外观与风格
    * [文本](文本.md)
    * [按钮](按钮.md)
    * [切换按钮](切换按钮.md)
    * [Pickers](Pickers.md)
    * [提示](提示.md)
  * 通知
    * [通知概览](通知概览.md)
  * [控制系统界面可见度](控制系统界面可见度.md)
  * [消息框概览](消息框概览.md)
  * [对话框](对话框.md)
  * [Menu](Menu.md)
  * [设置](设置.md)
  * [搜索](搜索.md)
  * [复制和粘贴](复制和粘贴.md)
  * [拖放](拖放.md)

* [动画和过渡](动画和过渡.md)
  
  * [动画lib](动画lib.md)

* 图片和图形
  
  * [Drawables overview](DrawablesOverview.md)
  * [Vector drawables overview](VectorDrawablesOverview.md)
  * [处理位图](处理位图.md)
  * [Hardware acceleration](HardwareAcceleration.md)
  * [Gallery](Gallery.md)

* 服务
  
  * [服务概览](服务概览.md)

* [权限](权限.md)
  
  * [权限概览](权限概览.md)
  * [请求应用权限](请求应用权限.md)

* App data & files
  
  * [保存到应用专属存储空间](保存到应用专属存储空间.md)
  * 保存到共享的存储空间
    * [访问共享存储空间中的媒体文件](访问共享存储空间中的媒体文件.md)
    * [从共享存储空间访问文档和其他文件](从共享存储空间访问文档和其他文件.md)
  * 将数据保存到本地数据库
    * [Room概述](Room概述.md)
    * [使用实体定义数据](使用实体定义数据.md)
    * [使用DAO访问数据](使用DAO访问数据.md)
    * [定义对象之间的关系](定义对象之间的关系.md)
    * [编写异步查询](编写异步查询.md)
    * [引用复杂数据](引用复杂数据.md)
  * [存储用例和最佳做法](存储用例和最佳做法.md)
  * 分享简单的数据
    * [将简单的数据发送给其他应用](将简单的数据发送给其他应用.md)
  * [分享文件](分享文件.md)
    * [设置文件共享](设置文件共享.md)
    * [共享文件](共享文件.md)
    * [请求某个分享的文件](请求某个分享的文件.md)
    * 检索文件信息
  * 内容提供程序
    * [内容提供程序基础知识](内容提供程序基础知识.md)
    * [创建内容提供程序](创建内容提供程序.md)
    * [使用存储访问框架打开文件](使用存储访问框架打开文件.md)
  * [缓存](缓存.md)

* [触摸和输入](触摸和输入.md)
  
  * [使用触摸手势](使用触摸手势.md)
    * [检测常用手势](检测常用手势.md)
  * [处理键盘输入](处理键盘输入.md)

* 连接性
  
  * 执行网络操作
    
    * [连接到网络](连接到网络.md)
    
    * 管理网络使用情况
    
    * 读取网络状态

* [基于网络的内容](基于网络的内容.md)
  
  * [WebView](WebView.md)

* [Android版本更新](Android版本更新.md)

* [App更新](App更新.md)

* lib
  
  * [Rxjava](Rxjava.md)
    * [Rxjava Opeartor](RxjavaOpeartor.md)
    * [Rx lib](RxLib.md)
  * [工具](工具.md)

* [绑定服务](绑定服务.md)
  
  * [Android 接口定义语言](Android 接口定义语言.md)

* [Broadcasts overview](Broadcasts overview.md)
  
  * Manage device awake state
    * [使设备保持唤醒状态](使设备保持唤醒状态.md)
  * [Jobscheduler](Jobscheduler.md)
+ Performance
  
  + Android vitals
    + [ANRs](ANRs.md)
    + [App startup time](App startup time.md)
  + [进程和线程](进程和线程.md)
  + [Better performance through threading](Better performance through threading.md)
    + Handler
      + [Android全面解析之Handler机制](Android全面解析之Handler机制.md)
  + 针对电池续航时间进行优化
    + [针对低电耗模式和应用待机模式进行优化](针对低电耗模式和应用待机模式进行优化.md)
  + [Manage your app memory](Manage your app memory.md)
    + [内存泄漏](内存泄漏.md)
  + [使应用能迅速响应](使应用能迅速响应.md)
  + [性能提示](性能提示.md)
