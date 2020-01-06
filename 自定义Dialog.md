# 自定义Dialog

## Dialog api

+ create()

+ onCreate(Bundle savedInstanceState)

  + ```xml
    <style name="Translucent_NoTitle" parent="android:style/Theme.Dialog">
            <item name="android:windowNoTitle">true</item>
            <item name="android:windowBackground">@android:color/transparent</item>
    </style>
    ```

+ show()

  + 判断宿主activity是否有效

+ onStart()

+ hide()

+ dismiss() cancel()

  + 宿主activity销毁时，dialog也需要销毁
  + dialog销毁时，dialog的引用应置为null

+ onStop()

+ setCanceledOnTouchOutside(boolean cancel)

  + 默认点击弹窗外部，执行cancel

## Dialog管理

+ [SmartAlertPop](https://github.com/PopFisher/SmartAlertPop)
+ 多个dialog显示时，同一时间只能显示一个dialog