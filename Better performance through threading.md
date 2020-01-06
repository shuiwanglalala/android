# Better performance through threading

## Main thread

对主线程很好的阐述

## Threads and UI object references

### Explicit references

we suggest that your app not include explicit references to UI objects in threaded work tasks

## Threads and app activity lifecycles

### Persisting threads

### Thread priority

Every time you create a thread, you should call setThreadPriority()

## Helper classes for threading

+ AsyncTask
  + a simple, useful primitive for apps that need to quickly move work from the main thread onto worker threads
  + For this reason, we suggest that you only use AsyncTask to handle work items shorter than 5ms in duration
  + you can use a WeakReference to store a reference to the required UI object
  + [Android AsyncTask完全解析，带你从源码的角度彻底理解](https://blog.csdn.net/guolin_blog/article/details/11711405)
+ HandlerThread
  + you may need a more traditional approach to executing a block of work on a longer running thread, and some ability to manage that workflow manually
  + don’t forget to set the thread’s priority based on the type of work it’s doing
  + [详解 Android 中的 HandlerThread](https://droidyue.com/blog/2015/11/08/make-use-of-handlerthread/)
