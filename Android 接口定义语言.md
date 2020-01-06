# Android 接口定义语言

## 定义 AIDL 接口

+ 创建 .aidl 文件
+ 实现接口
  + Android SDK 工具会生成一个以 .aidl 文件命名的 .java 接口文件。生成的接口包括一个名为 Stub 的子类，这个子类是其父接口的抽象实现，用于声明 .aidl 文件中的所有方法
+ 向客户端公开该接口
  + AIDL 接口的实现必须是完全线程安全实现
  + 默认情况下，RPC 调用是同步调用。如果您明知服务完成请求的时间不止几毫秒，就不应该从 Activity 的主线程调用服务，因为这样做可能会使应用挂起（Android 可能会显示“Application is Not Responding”对话框）— 您通常应该从客户端内的单独线程调用服务
  + 您引发的任何异常都不会回传给调用方
  + 当客户端在 onServiceConnected() 回调中收到 IBinder 时，它必须调用 YourServiceInterface.Stub.asInterface(service) 以将返回的参数转换成 YourServiceInterface 类型

## 通过 IPC 传递对象

通过 IPC 接口把某个类从一个进程发送到另一个进程是可以实现的。 不过，您必须确保该类的代码对 IPC 通道的另一端可用，并且该类必须支持 Parcelable 接口