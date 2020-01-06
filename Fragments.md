# Fragments

`Fragment` 表示 `Activity` 中的行为或用户界面部分

片段必须始终嵌入在 Activity 中，其生命周期直接受宿主 Activity 生命周期的影响

## 创建片段

### 向 Activity 添加片段

+ 在 Activity 的布局文件内声明片段
+ 或者通过编程方式将片段添加到某个现有 ViewGroup

## 执行片段事务

在您调用 commit() 之前，您可能想调用 addToBackStack()，以将事务添加到片段事务返回栈。 该返回栈由 Activity 管理，允许用户通过按返回按钮返回上一片段状态

如果您向事务添加了多个更改（如又一个 `add()` 或 `remove()`），并且调用了 `addToBackStack()`，则在调用`commit()` 前应用的所有更改都将作为单一事务添加到返回栈，并且*返回*按钮会将它们一并撤消

+ commit()
  + 不会立即执行事务，而是在 Activity 的 UI 线程（“主”线程）可以执行该操作时再安排其在线程上运行
+ executePendingTransactions()
  + 立即执行 commit() 提交的事务。通常不必这样做，除非其他线程中的作业依赖该事务
+ commitAllowingStateLoss()
  + [您只能在 Activity 保存其状态（用户离开 Activity）之前使用 commit() 提交事务。如果您试图在该时间点后提交，则会引发异常。 这是因为如需恢复 Activity，则提交后的状态可能会丢失。 对于丢失提交无关紧要的情况，请使用 commitAllowingStateLoss()](https://www.androiddesignpatterns.com/2013/08/fragment-transaction-commit-state-loss.html)

[failure-delivering-result-onactivityforresult](https://stackoverflow.com/questions/16265733/failure-delivering-result-onactivityforresult)

## 处理片段生命周期

|                     |                                                              |                                                              |
| ------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| onInflate           |                                                              |                                                              |
| onAttach            | Called when a fragment is first attached to its context      |                                                              |
| onCreate            | is not called if the fragment instance is retained across Activity re-creation | [setRetainInstance](https://blog.csdn.net/Gaugamela/article/details/56280384) |
| onCreateView        | Called to have the fragment instantiate its user interface view. This is optional, and non-graphical fragments can return null |                                                              |
| onViewCreated       | This gives subclasses a chance to initialize themselves once they know their view hierarchy has been completely created.  The fragment's view hierarchy is not however attached to its parent at this point |                                                              |
| onActivityCreated   | Called when the fragment's activity has been created and this fragment's view hierarchy instantiated |                                                              |
| onViewStateRestored |                                                              |                                                              |
| onStart             | This is generally tied to {@link Activity#onStart()} of the containing Activity's lifecycle |                                                              |
| onResume            | This is generally tied to {@link Activity#onResume()} of the containing Activity's lifecycle |                                                              |
| onPause             | This is generally tied to {@link Activity#onPause()} of the containing Activity's lifecycle |                                                              |
| onSaveInstanceState | this method may be called at any time before {@link #onDestroy()} |                                                              |
| onStop              | This is generally tied to {@link Activity#onStop()} of the containing Activity's lifecycle |                                                              |
| onDestroyView       | It is called regardless of whether {@link #onCreateView} returned a non-null view |                                                              |
| onDestroy           |                                                              | setRetainInstance                                            |
| onDetach            | Called when the fragment is no longer attached to its activity |                                                              |
|                     |                                                              |                                                              |
| setRetainInstance   | Control whether a fragment instance is retained across Activity re-creation (such as from a configuration change).  This can only be used with fragments not in the back stack |                                                              |
| getActivity         | Return the Activity this fragment is currently associated with |                                                              |

Activity 生命周期与片段生命周期之间的最显著差异在于它们在其各自返回栈中的存储方式。 默认情况下，Activity 停止时会被放入由系统管理的 Activity 返回栈（以便用户通过返回按钮回退到 Activity，任务和返回栈对此做了阐述）。不过，仅当您在移除片段的事务执行期间通过调用 addToBackStack() 显式请求保存实例时，系统才会将片段放入由宿主 Activity 管理的返回栈

片段所在的 Activity 的生命周期会直接影响片段的生命周期，其表现为，Activity 的每次生命周期回调都会引发每个片段的类似回调

[通过源码解析 Fragment 启动过程](https://www.jianshu.com/p/f2fcc670afd6)

[Activity/Fragment Purge and Restore Best Practices](Activity/Fragment Purge and Restore Best Practices)