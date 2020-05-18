# Understand the Activity Lifecycle

## Saving and restoring transient UI state

[`onSaveInstanceState()`](https://developer.android.com/reference/android/app/Activity?hl=zh-cn#onsaveinstancestate) is not called when the user explicitly closes the activity or in other cases when `finish()`is called

### Restore activity UI state using saved instance state

The system calls [`onRestoreInstanceState()`](https://developer.android.com/reference/android/app/Activity?hl=zh-cn#onrestoreinstancestate) only if there is a saved state to restore, so you do not need to check whether the [`Bundle`](https://developer.android.com/reference/android/os/Bundle?hl=zh-cn) is null

## 其他

[checking-if-an-android-application-is-running-in-the-background](https://stackoverflow.com/questions/3667022/checking-if-an-android-application-is-running-in-the-background/5862048#5862048)

[android-lifecycle](https://github.com/xxv/android-lifecycle)

|                        |                                                              |                                                              |                        |
| ---------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ---------------------- |
| onCreate               | initialization                                               | setContentView, findViewById、绑定UI更新监听                 |                        |
| onAttachFragment       |                                                              |                                                              |                        |
| onContentChanged       | the content view of the screen changes                       |                                                              | Window.Callback        |
| onStart                |                                                              |                                                              |                        |
| onRestoreInstanceState |                                                              | use your default implementation                              |                        |
| onPostCreate           | not for Applications                                         |                                                              |                        |
| onResume               | start interacting with the user                              | begin animations, open exclusive-access devices、刷新UI状态可变的控件 |                        |
| onPostResume           | not for Applications                                         |                                                              |                        |
| onAttachedToWindow     |                                                              |                                                              | Window.Callback        |
| onCreateOptionsMenu    |                                                              |                                                              |                        |
| onPause                | not do anything lengthy                                      | stop animations and other things that consume a noticeable amount of CPU in order to make the switch to the next activity as fast as possible |                        |
| onSaveInstanceState    | Save simple, lightweight UI state                            | record the transient state of the activity (the state of the UI) |                        |
| onStop                 | no longer visible to the user                                | store **persistent data** (such as data that should be saved to a database) |                        |
| onDestroy              | Perform any final cleanup, not a place for saving data       | free resources like threads、 handler、解绑UI更新监听        |                        |
| onRestart              |                                                              | load data                                                    |                        |
| onActivityResult       |                                                              |                                                              | startActivityForResult |
| onUserInteraction      | the user has interacted with the device in some way          |                                                              |                        |
| onUserLeaveHint        | an activity is about to go into the background as the result of user choice |                                                              |                        |
| onWindowFocusChanged   | the best indicator of whether this activity is visible to the user |                                                              | Window.Callback        |
| onDetachedFromWindow   |                                                              |                                                              | Window.Callback        |
| onNewIntent            |                                                              |                                                              | singleTop              |

