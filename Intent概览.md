# Intent概览

+ 作用
  + 启动activity
  + 启动service
  + 启动广播

+ Intent 类型
  + 显式 Intent
  + 隐式 Intent 
    + 为了确保应用的安全性，启动 Service 时，请始终使用显式 Intent，且不要为服务声明 Intent 过滤器

+ 构建 Intent
  + 组件名称
    + 构建显式 Intent 的一项重要信息，这意味着 Intent 应当仅传递给由组件名称定义的应用组件。如果没有组件名称，则 Intent 则为隐式
  + 