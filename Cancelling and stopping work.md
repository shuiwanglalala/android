# Cancelling and stopping work

Under the hood, WorkManager will check the State of the work. If the work is already finished, nothing will happen. Otherwise, its state will be changed to CANCELLED and the work will not run in the future. Any WorkRequests that are dependent on this work will also be CANCELLED

In addition, if the work is currently RUNNING, the worker will also receive a call to ListenableWorker.onStopped(). Override this method to handle any potential cleanup

## Stopping a running worker

+ You explicitly asked for it to be cancelled (by calling WorkManager.cancelWorkById(UUID), for example)
+ In the case of unique work, you explicitly enqueued a new WorkRequest with an ExistingWorkPolicy of REPLACE. The old WorkRequest is immediately considered terminated
+ Your work's constraints are no longer met
+ The system instructed your app to stop your work for some reason. This can happen if you exceed the execution deadline of 10 minutes. The work is scheduled for retry at a later time

Even if you signal completion of your work by returning a Result after onStopped() is called, WorkManager will ignore that Result because the worker is already considered stopped