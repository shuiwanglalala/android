# Fragment生命周期

A fragment's view has a separate `Lifecycle` that is managed independently from that of the fragment's `Lifecycle`. Fragments maintain a [`LifecycleOwner`](https://developer.android.com/reference/androidx/lifecycle/LifecycleOwner?hl=zh-cn) for their view, which can be accessed using [`getViewLifecycleOwner()`](https://developer.android.com/reference/androidx/fragment/app/Fragment?hl=zh-cn#getViewLifecycleOwner()) or [`getViewLifecycleOwnerLiveData()`](https://developer.android.com/reference/androidx/fragment/app/Fragment?hl=zh-cn#getViewLifecycleOwnerLiveData()). Having access to the view's `Lifecycle` is useful for situations where a Lifecycle-aware component should only perform work while a fragment's view exists, such as observing [`LiveData`](https://developer.android.com/topic/libraries/architecture/livedata?hl=zh-cn) that is only meant to be displayed on the screen.

## Fragments and the fragment manager

Beyond the fragment lifecycle, `FragmentManager` is also responsible for attaching fragments to their host activity and detaching them when the fragment is no longer in use. The `Fragment` class has two callback methods, `onAttach()` and `onDetach()`, that you can override to perform work when either of these events occur.

**Caution:** Avoid reusing `Fragment` instances after they are removed from the `FragmentManager`. While the fragment handles its own internal state cleanup, you might inadvertently carry over your own state into the reused instance.

## Fragment lifecycle states and callbacks

When determining a fragment's lifecycle state, `FragmentManager` considers the following:

- A fragment's maximum state is determined by its `FragmentManager`. A fragment cannot progress beyond the state of its `FragmentManager`.
- As part of a `FragmentTransaction`, you can set a maximum lifecycle state on a fragment using [`setMaxLifecycle()`](https://developer.android.com/reference/androidx/fragment/app/FragmentTransaction?hl=zh-cn#setMaxLifecycle(androidx.fragment.app.Fragment,%20androidx.lifecycle.Lifecycle.State)) .
- A fragment's lifecycle state can never be greater than its parent. For example, a parent fragment or activity must be started before its child fragments. Likewise, child fragments must be stopped before their parent fragment or activity.

**Caution:** Avoid using the `<fragment>` tag to add a fragment using XML, as the `<fragment>` tag allows a fragment to move beyond the state of its `FragmentManager`. Instead, always use [`FragmentContainerView`](https://developer.android.com/reference/androidx/fragment/app/FragmentContainerView?hl=zh-cn) for adding a fragment using XML.

### Upward state transitions

When moving upward through its lifecycle states, a fragment first calls the associated lifecycle callback for its new state. Once this callback is finished, the relevant [`Lifecycle.Event`](https://developer.android.com/reference/androidx/lifecycle/Lifecycle.Event?hl=zh-cn) is emitted to observers by the fragment's `Lifecycle`, followed by the fragment's view `Lifecycle`, if it has been instantiated.

#### Fragment and View STARTED

It is strongly recommended to tie [Lifecycle-aware components](https://developer.android.com/topic/libraries/architecture/lifecycle?hl=zh-cn) to the `STARTED` state of a fragment, as this state guarantees that the fragment's view is available, if one was created, and that it is safe to perform a `FragmentTransaction` on the child `FragmentManager` of the fragment.

### Downward state transitions

When a fragment moves downward to a lower lifecycle state, the relevant [`Lifecycle.Event`](https://developer.android.com/reference/androidx/lifecycle/Lifecycle.Event?hl=zh-cn) is emitted to observers by the fragment's view `Lifecycle`, if instantiated, followed by the fragment's `Lifecycle`. After a fragment's lifecycle event is emitted, the fragment calls the associated lifecycle callback.

#### Fragment and View CREATED

Once the fragment is no longer visible, the `Lifecycle`s for the fragment and for its view are moved into the `CREATED` state and emit the [`ON_STOP`](https://developer.android.com/reference/androidx/lifecycle/Lifecycle.Event?hl=zh-cn#ON_STOP) event to their observers. This state transition is triggered not only by the parent activity or fragment being stopped, but also by the saving of state by the parent activity or fragment. This behavior guarantees that the `ON_STOP` event is invoked before the fragment's state is saved. This makes the `ON_STOP` event the last point where it is safe to perform a `FragmentTransaction` on the child `FragmentManager`.
