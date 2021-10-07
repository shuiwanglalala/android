# Activity生命周期

https://github.com/xxv/android-lifecycle

## 保存和恢复瞬时界面状态

### 实例状态

**注意**：为了使 Android 系统恢复 Activity 中视图的状态，每个视图必须具有 `android:id` 属性提供的唯一 ID



https://github.com/JoseAlcerreca/android-lifecycles

[The Android Lifecycle cheat sheet — part I: Single Activities](https://medium.com/androiddevelopers/the-android-lifecycle-cheat-sheet-part-i-single-activities-e49fd3d202ab)

+ Single Activity — Scenario 1: App is finished and restarted
  + Triggered by
    + The user presses the Back button
    + The Activity.finish() method is called
  + `onSaveInstanceState` is not called (since the activity is finished, you don’t need to save state)
  + `onCreate` doesn’t have a Bundle when the app is reopened, because the activity was finished and the state doesn’t need to be restored
+ Single Activity — Scenario 2: User navigates away
  + Triggered by
    + The user presses the Home button
    + The user switches to another app (via Overview menu, from a notification, accepting a call, etc.)

+ Single Activity — Scenario 3: Configuration changes
  + Triggered by
    + Configuration changes, like a rotation
    + User resizes the window in multi-window mode
  + The activity is completely destroyed, but **the state is saved and restored for the new instance**.
  + The Bundle in `onCreate` and `onRestoreInstanceState` is the same
+ Single Activity — Scenario 4: App is paused by the system
  + Triggered by
    + Enabling Multi-window mode (API 24+) and losing the focus
    + Another app partially covers the running app (a purchase dialog, a runtime permission dialog, a third-party login dialog…)
    + An intent chooser appears, such as a share dialog
  + This scenario *doesn’t* apply to
    - Dialogs in the same app. Showing an `AlertDialog` or a `DialogFragment` won’t pause the underlying activity.
    - Notifications. User receiving a new notification or pulling down the notification bar won’t pause the underlying activity

[The Android Lifecycle cheat sheet — part II: Multiple activities](https://medium.com/androiddevelopers/the-android-lifecycle-cheat-sheet-part-ii-multiple-activities-a411fd139f24)

+ Navigating between activities
+ Activities in the back stack with configuration changes
+ App’s process is killed

[The Android Lifecycle cheat sheet — part III : Fragments](https://medium.com/androiddevelopers/the-android-lifecycle-cheat-sheet-part-iii-fragments-afc87d4f37fd)

+ Activity with Fragment starts and finishes

+ Activity with Fragment is rotated

  Fragment state is saved and restored in very similar fashion to activity state. The difference is that there’s no `onRestoreInstanceState` in fragments, but the Bundle is available in the fragment’s `onCreate`, `onCreateView` and `onActivityCreated`

+ Activity with retained Fragment is rotated

  Using retained fragments is not recommended unless they are used to store data across configuration changes (in a non-UI fragment). This is what the [ViewModel](https://developer.android.com/topic/libraries/architecture/viewmodel.html) class from the Architecture Components library uses internally, but with a simpler API

[The Android Lifecycle cheat sheet — part IV : ViewModels, Translucent Activities and Launch Modes](https://medium.com/androiddevelopers/the-android-lifecycle-cheat-sheet-part-iv-49946659b094)

+ ViewModels

+ Translucent Activities

  When the property `android:windowIsTranslucent` is applied to an activity’s theme, the diagram changes slightly: the background activity is never stopped, only paused, so it can continue receiving UI updates

+ Launch Modes