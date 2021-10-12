# Room概述

使用 [`@Database`](https://developer.android.com/reference/androidx/room/Database) 注释的类应满足以下条件

- 是扩展 [`RoomDatabase`](https://developer.android.com/reference/androidx/room/RoomDatabase) 的抽象类
- 在注释中添加与数据库关联的实体列表
- 包含具有 0 个参数且返回使用 [`@Dao`](https://developer.android.com/reference/androidx/room/Dao) 注释的类的抽象方法

**注意**：如果您的应用在单个进程中运行，在实例化 `AppDatabase` 对象时应遵循单例设计模式。每个 [`RoomDatabase`](https://developer.android.com/reference/androidx/room/RoomDatabase) 实例的成本相当高，而您几乎不需要在单个进程中访问多个实例

如果您的应用在多个进程中运行，请在数据库构建器调用中包含 `enableMultiInstanceInvalidation()`。这样，如果您在每个进程中都有一个 `AppDatabase` 实例，可以在一个进程中使共享数据库文件失效，并且这种失效会自动传播到其他进程中 `AppDatabase` 的实例