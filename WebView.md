# WebView

+ 在 WebView 中使用 JavaScript
  + 如果您将 targetSdkVersion 设置为 17 或更高，则必须向您希望 JavaScript（此方法也必须为公开方法）可用的任何方法添加 @JavascriptInterface 注释。如果您未提供注释，那么在 Android 4.2 或更高版本的平台上运行时您的网页将无法访问该方法
+ 处理网页导航
  + 当您的 WebView 替换网址加载时，它会自动累积已访问网页的历史记录。您可以使用 goBack() 和 goForward() 向后/向前浏览历史记录