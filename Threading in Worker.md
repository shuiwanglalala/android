# Threading in Worker

When you use a Worker, WorkManager automatically calls Worker.doWork() on a background thread

Note that Worker.doWork() is a synchronous call - you are expected to do the entirety of your background work in a blocking fashion and finish it by the time the method exits. If you call an asynchronous API in doWork() and return a Result, your callback may not operate properly. If you find yourself in this situation, consider using a ListenableWorker

Once a Worker has been stopped, it doesn't matter what you return from Worker.doWork(); the Result will be ignored