# 允许其他应用启动您的 Activity

+ 返回结果

  + 如果您想将结果返回给调用您 Activity 的 Activity，只需调用 setResult() 来指定结果代码和结果 Intent 即可。当您的操作完成且用户应返回原始 Activity 时，调用 finish() 关闭（并销毁）您的 Activity

    ```java
     // Create intent to deliver some kind of result data
     Intent result = new Intent("com.example.RESULT_ACTION", 	      Uri.parse("content://result_uri"));
     setResult(Activity.RESULT_OK, result);
     finish();
    ```

    + 默认情况下，结果设置为 RESULT_CANCELED。因此，如果用户在完成操作和您设置结果前按了“返回”按钮，原始 Activity 会收到“已取消”结果

  + 如果您只需返回指示若干结果选项之一的整数，则可以将结果代码设置为大于 0 的任何值。如果您使用结果代码传递整数，且无需包括 Intent，则可以调用 setResult() 并仅传递结果代码

    ```java
    setResult(RESULT_COLOR_RED);
    finish();
    ```