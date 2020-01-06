# ViewModel

## Implement a ViewModel

A ViewModel must never reference a view, Lifecycle, or any class that may hold a reference to the activity context

ViewModel objects can contain LifecycleObservers, such as LiveData objects. However ViewModel objects must never observe changes to lifecycle-aware observables, such as LiveData objects. If the ViewModel needs the Application context, for example to find a system service, it can extend the AndroidViewModel class and have a constructor that receives the Application in the constructor, since Application class extends Context

## The lifecycle of a ViewModel

The ViewModel remains in memory until the Lifecycle it's scoped to goes away permanently: in the case of an activity, when it finishes, while in the case of a fragment, when it's detached

## Share data between fragments





[Android官方架构组件ViewModel:从前世今生到追本溯源](https://juejin.im/post/5c047fd3e51d45666017ff86)