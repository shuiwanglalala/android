# Optimizing the View

In particular you should eliminate allocations in `onDraw()`, because allocations may lead to a garbage collection that would cause a stutter. Allocate objects during initialization, or between animations. Never make an allocation while an animation is running

In addition to making `onDraw()` leaner, also make sure it's called as infrequently as possible. Most calls to `onDraw()` are the result of a call to `invalidate()`, so eliminate unnecessary calls to `invalidate()`

These deep view hierarchies cause performance problems. Make your view hierarchies as shallow as possible

If you have a complex UI, consider writing a custom `ViewGroup` to perform its layout. Unlike the built-in views, your custom view can make application-specific assumptions about the size and shape of its children, and thus avoid traversing its children to calculate measurements