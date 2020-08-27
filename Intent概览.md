# Intent概览

+ Intent 是一个消息传递对象，您可以用来从其他应用组件请求操作
  
  + 启动activity
  + 启动service
  + 启动广播
  
+ Intent 类型
  + 显式 Intent
  + 隐式 Intent 
    
    + 为了确保应用的安全性，启动 Service 时，请始终使用显式 Intent，且不要为服务声明 Intent 过滤器
      
    + 用户可能没有任何应用处理您发送到 startActivity() 的隐式 Intent。或者，由于配置文件限制或管理员执行的设置，可能无法访问应用。如果发生这样的情况，调用失败，应用也会崩溃。要验证 Activity 是否会接收 Intent，请对 Intent 对象调用 resolveActivity()。如果结果为非空，则至少有一个应用能够处理该 Intent，并且可以安全调用 startActivity()。如果结果为空，不要使用该 Intent。如有可能，您应停用发出该 Intent 的功能
    
      ```java
          PackageManager packageManager = getPackageManager();
          List<ResolveInfo> activities = packageManager.queryIntentActivities(intent,
                  PackageManager.MATCH_DEFAULT_ONLY);
          boolean isIntentSafe = activities.size() > 0;
      ```
  
+ 构建 Intent
  
  + （组件名称、操作、数据和类别）表示 Intent 的既定特征。通过读取这些属性，Android 系统能够解析应当启动哪个应用组件
    
    + 组件名称
      + 构建显式 Intent 的一项重要信息，这意味着 Intent 应当仅传递给由组件名称定义的应用组件。如果没有组件名称，则 Intent 则为隐式
    + 操作 指定要执行的通用操作（例如，*查看*或*选取*）的字符串
    + 数据
      + 引用待操作数据和/或该数据 MIME 类型的 URI（Uri 对象）。提供的数据类型通常由 Intent 的操作决定
      + 若要同时设置 URI 和 MIME 类型，请勿调用 setData() 和 setType()，因为它们会互相抵消彼此的值。请始终使用 setDataAndType() 同时设置 URI 和 MIME 类型
    + 类别 一个包含应处理 Intent 组件类型的附加信息的字符串
    
  + Intent 也有可能会携带一些不影响其如何解析为应用组件的信息
  
    + Extra 携带完成请求操作所需的附加信息的键值对
      + 使用各种 putExtra() 方法添加 extra 数据，每种方法均接受两个参数：键名和值
      + 还可以创建一个包含所有 extra 数据的 Bundle 对象，然后使用 putExtras() 将 Bundle 插入 Intent 中
    + 标志 标志在 Intent 类中定义，充当 Intent 的元数据
  
  + 强制使用应用选择器
  
    ```java
    Intent sendIntent = new Intent(Intent.ACTION_SEND);
    ...
    
    // Always use string resources for UI text.
    // This says something like "Share this photo with"
    String title = getResources().getString(R.string.chooser_title);
    // Create intent to show the chooser dialog
    Intent chooser = Intent.createChooser(sendIntent, title);
    
    // Verify the original intent will resolve to at least one activity
    if (sendIntent.resolveActivity(getPackageManager()) != null) {
        startActivity(chooser);
    }
    ```

+ Intent 解析
  + 操作测试
    + 要通过此过滤器，您在 Intent 中指定的操作必须与过滤器中列出的某一操作匹配
    + 如果该过滤器未列出任何操作，则 Intent 没有任何匹配项，因此所有 Intent 均无法通过测试。但是，如果 Intent 未指定操作，则只要过滤器内包含至少一项操作，就可以通过测试
  + 类别测试
    + 若要使 Intent 通过类别测试，则 Intent 中的每个类别均必须与过滤器中的类别匹配。反之则未必然，Intent 过滤器声明的类别可以超出 Intent 中指定的数量，且 Intent 仍会通过测试。因此，不含类别的 Intent 应当始终会通过此测试，无论过滤器中声明何种类别均是如此
  + 数据测试
    + 仅当过滤器未指定任何 URI 或 MIME 类型时，不含 URI 和 MIME 类型的 Intent 才会通过测试
    + 对于包含 URI 但不含 MIME 类型（既未显式声明，也无法通过 URI 推断得出）的 Intent，仅当其 URI 与过滤器的 URI 格式匹配、且过滤器同样未指定 MIME 类型时，才会通过测试
    + 仅当过滤器列出相同的 MIME 类型且未指定 URI 格式时，包含 MIME 类型但不含 URI 的 Intent 才会通过测试
    + 仅当 MIME 类型与过滤器中列出的类型匹配时，同时包含 URI 类型和 MIME 类型（通过显式声明，或可以通过 URI 推断得出）的 Intent 才会通过测试的 MIME 类型部分。如果 Intent 的 URI 与过滤器中的 URI 匹配，或者如果 Intent 具有 content: 或 file: URI 且过滤器未指定 URI，则 Intent 会通过测试的 URI 部分。换言之，如果过滤器只是列出 MIME 类型，则假定组件支持 content: 和 file: 数据

+ 接收隐式 Intent
  + 显式 Intent 始终会传递给其目标，无论组件声明的 Intent 过滤器如何均是如此
  + 要接收隐式 Intent，必须将 CATEGORY_DEFAULT 类别包括在 Intent 过滤器中。方法 startActivity() 和 startActivityForResult() 将按照其声明 CATEGORY_DEFAULT 类别的方式处理所有 Intent
  + 使用 Intent 过滤器时，无法安全地防止其他应用启动组件。尽管 Intent 过滤器将组件限制为仅响应特定类型的隐式 Intent，但如果开发者确定您的组件名称，则其他应用有可能通过使用显式 Intent 启动您的应用组件。如果必须确保只有您自己的应用才能启动您的某一组件，请勿在您的清单中声明 Intent 过滤器。而是将该组件的 exported 属性设置为 "false"
  + 对于所有 Activity，您必须在清单文件中声明 Intent 过滤器。但是，广播接收器的过滤器可以通过调用 registerReceiver() 动态注册。稍后，您可以使用 unregisterReceiver() 注销该接收器。这样一来，应用便可仅在应用运行时的某一指定时间段内侦听特定的广播