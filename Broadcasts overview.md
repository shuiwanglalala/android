# Broadcasts overview

## Receiving broadcasts

### Manifest-declared receivers

If you declare a broadcast receiver in your manifest, the system launches your app (if the app is not already running) when the broadcast is sent

The system creates a new BroadcastReceiver component object to handle each broadcast that it receives. This object is valid only for the duration of the call to onReceive(Context, Intent). Once your code returns from this method, the system considers the component no longer active

### Context-registered receivers

Context-registered receivers receive broadcasts as long as their registering context is valid. For an example, if you register within an `Activity` context, you receive broadcasts as long as the activity is not destroyed. If you register with the Application context, you receive broadcasts as long as the app is running

To stop receiving broadcasts, call `unregisterReceiver(android.content.BroadcastReceiver)`. Be sure to unregister the receiver when you no longer need it or the context is no longer valid

### Effects on process state

## Sending broadcasts

+ sendOrderedBroadcast(Intent, String)
  + sends broadcasts to one receiver at a time. As each receiver executes in turn, it can propagate a result to the next receiver, or it can completely abort the broadcast so that it won't be passed to other receivers
+ sendBroadcast(Intent)
  + sends broadcasts to all receivers in an undefined order
+ LocalBroadcastManager.sendBroadcast
  + If you don't need to send broadcasts across apps, use local broadcasts

## Restricting broadcasts with permissions



[用广播 BroadcastReceiver 更新 UI 界面真的好吗？](https://juejin.im/entry/59f91bc0f265da430405ee79)

[前台广播——解决广播接收延时问题](https://blog.csdn.net/m_xiaoer/article/details/72860200)