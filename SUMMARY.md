# Summary

* [Todo](Todo.md)

* software
  
  * 编写您的应用
    
    * 添加多密度矢量图形
    
    * 使用 lint 检查改进您的代码
    
    * 工具属性参考文档
  
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

* Material Design
  
  * [Material库](Material库.md)

* 设备兼容性
  
  * [设备兼容性概览](设备兼容性概览.md)
  
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

* 应用导航
  
  * Navigation组件
    
    * [Navigation组件使用入门](Navigation组件使用入门.md)
    
    * [创建目的地](创建目的地.md)
    
    * [嵌套导航图](嵌套导航图.md)
    
    * [支持多个返回堆栈](支持多个返回堆栈.md)
    
    * [条件导航](条件导航.md)
    
    * [使用 NavigationUI 更新界面组件](使用NavigationUI更新界面组件.md)
  
  * Fragment
    
    * [创建Fragment](创建Fragment.md)
    
    * [Fragment管理器](Fragment管理器.md)
    
    * [Fragment事务](Fragment事务.md)
    
    * [Fragment生命周期](Fragment生命周期.md)
    
    * [与Fragment通信](与Fragment通信.md)
    
    * [DialogFragment](DialogFragment.md)
    
    * [调试Fragment](调试Fragment.md)
  
  * 应用链接
    
    * [创建指向应用内容的深层链接](创建指向应用内容的深层链接.md)
    
    * [验证Android应用链接](验证Android应用链接.md)
  
  * [ViewPager2](ViewPager2.md)
  
  * [提供自定义返回导航](提供自定义返回导航.md)

* [依赖项注入](依赖项注入.md)
  
  * [使用Hilt实现依赖项注入](使用Hilt实现依赖项注入.md)

* 与其他应用交互
  
  * [与其他应用交互概览](与其他应用交互概览.md)
  
  * [向另一个应用发送用户](向另一个应用发送用户.md)
  
  * [获取activity的结果](获取activity的结果.md)
  
  * [允许其他应用启动您的 Activity](允许其他应用启动您的Activity.md)
  
  * 软件包可见性

* Intent和Intent过滤器
  
  * Intent概览
  
  * 常见Intent

* 界面
  
  * [布局](布局.md)
    
    * [ConstraintLayout](ConstraintLayout.md)
    
    * [RecyclerView](RecyclerView.md)
      
      * [RecyclerView缓存机制](RecyclerView缓存机制.md)
    
    * [自定义视图组件](自定义视图组件.md)
  
  * 外观与风格
    
    * [样式和主题背景](样式和主题背景.md)
    
    * [文本](文本.md)
      
      * 自动调整textview大小
      
      * Span
    
    * [Pickers](Pickers.md)
    
    * [提示](提示.md)
  
  * [启动画面](启动画面.md)
  
  * [窗口边衬区](窗口边衬区.md)
  
  * [支持滑动刷新](支持滑动刷新.md)
  
  * [Menu](Menu.md)
  
  * [搜索](搜索.md)

* [动画和过渡](动画和过渡.md)
  
  * [动画lib](动画lib.md)

* 图片和图形
  
  * [可绘制对象概览](可绘制对象概览.md)
  
  * [矢量可绘制对象概览](矢量可绘制对象概览.md)
  
  * [处理位图](处理位图.md)
  
  * [ImageView](ImageView.md)
  
  * [Photo](Photo.md)

* 服务
  
  * [服务概览](服务概览.md)

* 后台任务
  
  * [后台任务概览](后台任务概览.md)
  
  * 广播
    
    * [广播概览](广播概览.md)

* 权限
  
  * [权限概览](权限概览.md)
  
  * [请求应用权限](请求应用权限.md)
  
  * 限制与其他应用的交互

* 应用数据与文件
  
  * [应用数据与文件概览](应用数据与文件概览.md)
  
  * [访问应用专属文件](访问应用专属文件.md)
  
  * [保存键值对](保存键值对.md)
  
  * [保存到本地数据库](保存到本地数据库.md)
  
  * Android存储用例和最佳做法
  
  * [缓存](缓存.md)

* 用户数据和身份
  
  * 检查您的应用如何收集和分享用户数据

* 触摸和输入
  
  * [输入事件](输入事件.md)
  
  * 使用触摸手势
    
    * [检测常用手势](检测手势.md)
    
    * 在ViewGroup中管理轻触事件
  
  * [使用键盘输入](使用键盘输入.md)
    
    * 指定输入法类型
    
    * 处理输入法可见性

* 连接性
  
  * 执行网络操作
    
    * [连接到网络](连接到网络.md)
    
    * 管理网络使用情况
    
    * 读取网络状态

* 基于网络的内容
  
  * [基于网络的内容概览](基于网络的内容概览.md)
  
  * 在WebView中编译Web应用

* 性能
  
  * 提高性能
    
    * 解决常见问题
      
      * 缩减应用大小

* 其他
  
  * [Android全面解析之Handler机制](Android全面解析之Handler机制.md)
  
  * [Window](Window.md)
  
  * [View](View.md)
    
    * [View绘制](View绘制.md)
  
  * [Rxjava](Rxjava.md)
    
    * [Rxjava Opeartor](RxjavaOpeartor.md)
    
    * [Rx lib](RxLib.md)
  
  * [事件总线](事件总线.md)
