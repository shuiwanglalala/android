# 使用DAO访问数据

DAO 既可以是接口，也可以是抽象类。如果是抽象类，则该 DAO 可以选择有一个以 [`RoomDatabase`](https://developer.android.com/reference/androidx/room/RoomDatabase) 为唯一参数的构造函数。Room 会在编译时创建每个 DAO 实现

## 定义方法以方便使用

### 插入

当您创建 DAO 方法并使用 [`@Insert`](https://developer.android.com/reference/androidx/room/Insert) 对其进行注释时，Room 会生成一个实现，该实现在单个事务中将所有参数插入数据库中

如果 [`@Insert`](https://developer.android.com/reference/androidx/room/Insert) 方法只接收 1 个参数，则它可以返回 `long`，这是插入项的新 `rowId`。如果参数是数组或集合，则应返回 `long[]` 或 `List`

## 查询信息

[`@Query`](https://developer.android.com/reference/androidx/room/Query) 是 DAO 类中使用的主要注释。它允许您对数据库执行读/写操作。每个 [`@Query`](https://developer.android.com/reference/androidx/room/Query) 方法都会在编译时进行验证，因此如果查询出现问题，则会发生编译错误，而不是运行时失败

Room 还会验证查询的返回值，以确保当返回的对象中的字段名称与查询响应中的对应列名称不匹配时，Room 可以通过以下两种方式之一提醒您

- 如果只有部分字段名称匹配，则会发出警告
- 如果没有任何字段名称匹配，则会发出错误

### 直接光标访问

**注意**：强烈建议不要使用 Cursor API，因为它无法保证行是否存在或者行包含哪些值。只有当您已具有需要光标且无法轻松重构的代码时，才使用此功能

## 查询返回类型

### 使用流进行响应式查询

暂不了解，还有room-ktx

https://medium.com/androiddevelopers/room-flow-273acffe5b57

### 使用 Kotlin 协程进行异步查询

您可以将 `suspend` Kotlin 关键字添加到 DAO 方法中，以使用 Kotlin 协程功能使这些方法成为异步方法。这样可确保不会在主线程上执行这些方法

本指南也适用于带有 [`@Transaction`](https://developer.android.com/reference/androidx/room/Transaction) 注释的 DAO 方法。您可以使用此功能通过其他 DAO 方法构建暂停数据库方法。然后，这些方法会在单个数据库事务中运行

**注意**：应避免在单个数据库事务中执行额外的应用端工作，因为 Room 会将此类事务视为独占事务，并且按顺序每次仅执行一个事务。这意味着，包含不必要操作的事务很容易会锁定您的数据库并影响性能

### 使用 LiveData 进行可观察查询

### 使用 RxJava 进行响应式查询

https://medium.com/androiddevelopers/room-rxjava-acb0cd4f3757

文章很详细，对各类情况均有说明

https://github.com/android/architecture-components-samples/tree/master/BasicRxJavaSample

https://github.com/android/architecture-components-samples/tree/master/BasicRxJavaSampleKotlin

两个demo的内容一样，一个java版本，一个kotlin版本