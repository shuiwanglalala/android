# 允许其他应用启动您的 Activity

## 添加 intent 过滤器

注意：为了接收隐式 intent，您必须在 intent 过滤器中添加 CATEGORY_DEFAULT 类别。startActivity() 和 startActivityForResult() 方法将所有 intent 当作声明了 CATEGORY_DEFAULT 类别一样对待。如果您没有在 intent 过滤器中声明该类别，任何隐式 intent 都不会解析为您的 activity。

## 处理您的 activity 中的 intent

当您的 activity 启动时，调用 getIntent() 以检索启动 activity 的 Intent。您可以在 activity 生命周期的任何时间执行此操作，但通常应在早期回调（例如，onCreate() 或 onStart()）时执行。

## 返回结果

如果您想将结果返回给调用您 activity 的 activity，只需调用 setResult() 来指定结果代码和结果 Intent 即可。当您的操作完成且用户应返回原始 activity 时，调用 finish() 以关闭（并销毁）您的 activity。

您必须始终为结果指定结果代码。通常，结果代码是 RESULT_OK 或 RESULT_CANCELED。之后您可以根据需要使用 Intent 提供额外的数据。

如果您只需返回指示若干结果选项之一的整数，则可以将结果代码设置为大于 0 的任何值。如果您使用结果代码传递整数，且无需包括 Intent，则可以调用 setResult() 并仅传递结果代码。