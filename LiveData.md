# LiveData

LiveData considers an observer, which is represented by the Observer class, to be in an active state if its lifecycle is in the STARTED or RESUMED state

## Work with LiveData objects

### Observe LiveData objects

In most cases, an app component’s onCreate() method is the right place to begin observing a LiveData object

Generally, LiveData delivers updates only when data changes, and only to active observers. An exception to this behavior is that observers also receive an update when they change from an inactive to an active state

After observe() is called with nameObserver passed as parameter, onChanged() is immediately invoked providing the most recent value stored in mCurrentName. If the LiveData object hasn't set a value in mCurrentName, onChanged() is not called

### Use LiveData with Room

The Room persistence library supports observable queries, which return LiveData objects. Observable queries are written as part of a Database Access Object (DAO)

Room generates all the necessary code to update the LiveData object when a database is updated

## Extend LiveData

The fact that LiveData objects are lifecycle-aware means that you can share them between multiple activities, fragments, and services. To keep the example simple, you can implement the LiveData class as a singleton

## Transform LiveData

类似rajava操作符

很好的例子

## Merge multiple LiveData sources

Transformations和MediatorLiveData，注意部分方法均必须在主线程调用



