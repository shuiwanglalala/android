# MotionLayout

https://github.com/android/views-widgets-samples/tree/master/ConstraintLayoutExamples

非常棒的动画机制

https://medium.com/google-developers/introduction-to-motionlayout-part-i-29208674b10d

A mix between the property animation framework, layout transitions with TransitionManager, and CoordinatorLayout

+ Limitations

MotionLayout will only provide its capabilities for its direct children — contrary to TransitionManager, which can work with nested layout hierarchies as well as Activity transitions

+ When to use it

Use MotionLayout when animating UI elements the user will interact with

+ OnSwipe handler

`touchAnchorId`: the object we should track (here, `@+id/button`)

`touchAnchorSide`: the side of the object that should track your finger (`right / left / top / bottom`)

`dragDirection`: the direction of the motion we are tracking (`dragRight / dragLeft / dragUp / dragDown` will define how the progress value will be set, from 0 to 1)

+ ConstraintSet

One important thing to keep in mind is how ConstraintSet works — they will replace all existing constraints of the affected widgets

On the other hand, let’s say that you have a layout with a dozen widgets, but only one that you are animating — the ConstraintSet in MotionScene only need to contain the Constraint for that one widget

https://medium.com/google-developers/introduction-to-motionlayout-part-ii-a31acc084f59

+ ImageFilterView

https://medium.com/google-developers/introduction-to-motionlayout-part-iii-47cd64d51a5

https://medium.com/google-developers/defining-motion-paths-in-motionlayout-6095b874d37