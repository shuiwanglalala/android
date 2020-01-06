# Tasks and Back Stack

A task is a collection of activities that users interact with when performing a certain job

A task is a cohesive unit that can move to the "background" when users begin a new task or go to the Home screen

the activities in the back stack are never rearranged

## Managing Tasks

Launch modes allow you to define how a new instance of an activity is associated with the current task

Activity A's request (as defined in the intent) is honored over Activity B's request (as defined in its manifest)

------

|                                    |                |                                                              |                                                              |
| ---------------------------------- | -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| FLAG_ACTIVITY_SINGLE_TOP           | singleTop      |                                                              |                                                              |
| FLAG_ACTIVITY_NEW_TASK             | singleTask     | Only one instance of the activity can exist at a time        |                                                              |
|                                    | singleInstance | The activity is always the single and only member of its task |                                                              |
| FLAG_ACTIVITY_CLEAR_TOP            |                |                                                              | FLAG_ACTIVITY_NEW_TASK                                       |
| FLAG_ACTIVITY_RESET_TASK_IF_NEEDED |                |                                                              | [what-are-the-differences-between-flag-activity-reset-task-if-needed-and-flag-act](https://stackoverflow.com/questions/29321261/what-are-the-differences-between-flag-activity-reset-task-if-needed-and-flag-act) |
| FLAG_ACTIVITY_REORDER_TO_FRONT     |                |                                                              |                                                              |
| FLAG_ACTIVITY_CLEAR_TASK           |                |                                                              | FLAG_ACTIVITY_NEW_TASK                                       |

### Handling affinities

The *affinity* indicates which task an activity prefers to belong to. By default, all the activities from the same app have an affinity for each other

+ When the intent that launches an activity contains the `FLAG_ACTIVITY_NEW_TASK` flag
+ When an activity has its [`allowTaskReparenting`](https://developer.android.com/guide/topics/manifest/activity-element.html?hl=zh-cn#reparent) attribute set to `"true"`

### Clearing the back stack

If the user leaves a task for a long time, the system clears the task of all activities except the root activity. When the user returns to the task again, only the root activity is restored

+ alwaysRetainTaskState
  + The task retains all activities in its stack even after a long period
+ clearTaskOnLaunch
  + the stack is cleared down to the root activity whenever the user leaves the task and returns to it
+ finishOnTaskLaunch
  + This attribute is like [`clearTaskOnLaunch`](https://developer.android.com/guide/topics/manifest/activity-element.html?hl=zh-cn#clear), but it operates on a single activity, not an entire task

### Starting a task

the two launch modes that mark activities as always initiating a task, `"singleTask"` and`"singleInstance"`, should be used only when the activity has an `ACTION_MAIN` and a `CATEGORY_LAUNCHER` filter

## 其他

[view-the-tasks-activity-stack](https://stackoverflow.com/questions/2442713/view-the-tasks-activity-stack)

[ActivityTaskView](https://github.com/shuiwanglalala/ActivityTaskView)

自定义stack

+ [关于获取当前Activity的一些思考](https://droidyue.com/blog/2016/02/21/thinking-of-getting-the-current-activity-in-android/)

  