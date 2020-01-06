# ANRs

## Detect and diagnose problems

### Diagnosing ANRs

[Strict mode](https://droidyue.com/blog/2015/09/26/android-tuning-tool-strictmode/)

## Fix the problems

+ Slow code on the main thread
+ IO on the main thread
+ Lock contention
  + If a worker thread holds a lock on a resource that the main thread requires to complete its work, then an ANR might happen
+ Deadlocks
+ Slow broadcast receivers



[Android性能优化（七）之你真的理解ANR吗？](https://juejin.im/post/58e5bd6dda2f60005fea525c)

[Android ANR日志分析指南](https://juejin.im/post/5be698d4e51d452acb74ea4c)

+ binder数据量过大
+ binder通信失败

[Android - how do I investigate an ANR?](https://stackoverflow.com/questions/704311/android-how-do-i-investigate-an-anr)

[how-to-read-dalvik-sigquit-output](http://elliotth.blogspot.com/2012/08/how-to-read-dalvik-sigquit-output.html)

