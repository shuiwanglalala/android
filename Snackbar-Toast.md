# Snackbar-Toast

[Toast](https://developer.android.com/guide/topics/ui/notifiers/toasts)

[Snackbar](https://developer.android.com/training/snackbar)

**Snackbar 类取代了 Toast。虽然目前仍支持 Toast，但现在首选使用 Snackbar 向用户显示简短的瞬时消息**

```java
Snackbar mySnackbar = Snackbar.make(view, stringId, duration);
mySnackbar.setAction(R.string.undo_string, new MyUndoListener());
```

view

Snackbar 附加到的视图。该方法实际上会从传递的视图中往上搜索视图层次结构，直到到达 CoordinatorLayout 或窗口装饰的内容视图。通常，仅传递封装您的内容的 CoordinatorLayout 最为简单

系统不会同时显示多个 Snackbar 对象，因此，如果视图当前显示的是另一个 Snackbar，则系统会将您的 Snackbar 加入队列，并在当前 Snackbar 过期或关闭后显示它

[Android SnackBar: error inflating SnackbarLayout](https://stackoverflow.com/questions/30612985/android-snackbar-error-inflating-snackbarlayout/30613179)