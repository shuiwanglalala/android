# Background Tasks

|            | Thread                | Timer                                                      | AsyncTask                                              | Handler                                 | HandlerThread                                                | Service                    | 前台服务                         | 后台服务 | IntentService                                | 绑定服务   | jobscheduler               | AlarmManager                   | RxJava             |            |
| ---------- | --------------------- | ---------------------------------------------------------- | ------------------------------------------------------ | --------------------------------------- | ------------------------------------------------------------ | -------------------------- | -------------------------------- | -------- | -------------------------------------------- | ---------- | -------------------------- | ------------------------------ | ------------------ | ---------- |
| 设计理念   |                       | schedule tasks for future execution in a background thread | a helper class around Thread and Handler               | 1.未来某个时间点处理 Messages；2.切线程 | A Thread that has a Looper. The Looper can then be used to create Handlers | 执行长时间操作而不提供界面 | 请限制应用使用前台服务           | 26有限制 | 使用工作线程逐一处理所有启动请求             |            | 条件触发，批量处理后台任务 | 在应用生命周期之外定时执行操作 |                    | 设计理念   |
| 线程切换   |                       | 子线程内执行                                               | 可以；任务处理后，支持主线程回调                       | 可以                                    | 可以                                                         | 不支持                     | 不支持                           |          | 支持                                         | 不支持     | 不支持                     | 不支持                         | 随便切             | 线程切换   |
| 运行时间   | 无限制，等待终止信号  |                                                            | 不超过5ms                                              |                                         | 无限制                                                       |                            | 无限制                           |          |                                              | 无限制     | 无限制                     |                                |                    | 运行时间   |
| 结束方式   | Runtime.exit/扔出异常 | 执行完task/cancel()                                        | invoking cancel(boolean)                               | removeCallbacks                         |                                                              |                            | stopSelf                         |          |                                              | 无组件绑定 |                            |                                | onError/onComplete | 结束方式   |
| 打断后恢复 |                       |                                                            |                                                        |                                         |                                                              |                            | onStartCommand返回值决定是否粘性 |          |                                              |            | 支持（包括重启）           | 支持                           |                    | 打断后恢复 |
| 顺序执行   |                       |                                                            |                                                        | 可以                                    |                                                              |                            |                                  |          |                                              |            |                            |                                | 操作符支持         | 顺序执行   |
| 循环       |                       | 可以                                                       |                                                        | 可以                                    |                                                              |                            |                                  |          |                                              |            | 支持                       |                                | 操作符支持         | 循环       |
| 定时       |                       | 可以                                                       |                                                        | 可以                                    |                                                              |                            |                                  |          |                                              |            | 支持                       | 支持                           | 操作符支持         | 定时       |
| 跨进程通信 |                       |                                                            |                                                        |                                         |                                                              |                            |                                  |          |                                              | AIDL       |                            |                                |                    | 跨进程通信 |
| 使用限制   | 设置线程优先级        | Timer tasks should complete quickly                        | The task can be executed only once；不允许并行任务执行 |                                         | 设置线程优先级                                               |                            |                                  |          | 无法操作UI；只能同步顺序执行；操作无法被打断 |            | sdk>23                     |                                |                    | 使用限制   |
| 其他       |                       | 线程安全                                                   | WeakReference持有UI                                    |                                         |                                                              |                            |                                  |          |                                              |            |                            | 与广播接收器结合使用           |                    | 其他       |
|            |                       |                                                            |                                                        |                                         |                                                              |                            |                                  |          |                                              |            |                            |                                |                    |            |



[Android 中的定时任务调度](https://juejin.im/post/595c9061f265da6c22119084)

[从Service到WorkManager](https://juejin.im/post/5b04d064f265da0b80711759)