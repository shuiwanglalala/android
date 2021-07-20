# DataStore

**注意**：如果您需要支持大型或复杂数据集、部分更新或参照完整性，请考虑使用 [Room](https://developer.android.com/training/data-storage/room)，而不是 DataStore。DataStore 非常适合简单的小型数据集，不支持部分更新或参照完整性

## 设置

**注意**：如果您将 `datastore-preferences-core` 工件与 Proguard 搭配使用，就必须手动将 Proguard 规则添加到 `proguard-rules.pro` 文件中，以免您的字段遭到删除。您可以点击[此处](https://cs.android.com/androidx/platform/frameworks/support/+/androidx-main:datastore/datastore-preferences/proguard-rules.pro)查找必要的规则

## 在同步代码中使用 DataStore

**注意**：请尽可能避免在 DataStore 数据读取时阻塞线程。阻塞界面线程可能会导致 [ANR](https://developer.android.com/topic/performance/vitals/anr) 或界面卡顿，而阻塞其他线程可能会导致[死锁](https://en.wikipedia.org/wiki/Deadlock)

## 其他资源

- [使用 Preferences DataStore](https://codelabs.developers.google.com/codelabs/android-preferences-datastore)
  - 事务性操作很好

- [使用 Proto DataStore](https://codelabs.developers.google.com/codelabs/android-proto-datastore)
  - 未下载





[再见 SharedPreferences 拥抱 Jetpack DataStore（一）](https://juejin.im/post/6881442312560803853)

- datastore的版本很早，api有变动
- 依赖注入 数据驱动UI 很好
- MMKV值得后续了解

[再见 SharedPreferences 拥抱 DataStore (二)](https://juejin.im/post/6888847647802097672)

[反思｜官方也无力回天？Android SharedPreferences的设计与实现](https://juejin.cn/post/6884505736836022280#heading-10)