# Fragment事务

## Adding and removing fragments

**Note:** It is strongly recommended to always use fragment operations that take a `Class` rather than a fragment instance to ensure that the same mechanisms for creating the fragment are also used for restoring the fragment from a saved state.

### Commit is asynchronous

Calling [`commit()`](https://developer.android.com/reference/androidx/fragment/app/FragmentTransaction?hl=zh-cn#commit()) doesn't perform the transaction immediately. Rather, the transaction is scheduled to run on the main UI thread as soon as it is able to do so. If necessary, however, you can call [`commitNow()`](https://developer.android.com/reference/androidx/fragment/app/FragmentTransaction?hl=zh-cn#commit()) to run the fragment transaction on your UI thread immediately.

Note that `commitNow` is incompatible with `addToBackStack`. Alternatively, you can execute all pending `FragmentTransactions` submitted by [`commit()`](https://developer.android.com/reference/androidx/fragment/app/FragmentTransaction?hl=zh-cn#commit()) calls that have not yet run by calling [`executePendingTransactions()`](https://developer.android.com/reference/androidx/fragment/app/FragmentManager?hl=zh-cn#executePendingTransactions()). This approach is compatible with `addToBackStack`.

For the vast majority of use cases, `commit()` is all you need.

## Limit the fragment's lifecycle

`FragmentTransactions` can affect the lifecycle state of individual fragments added within the scope of the transaction. When creating a `FragmentTransaction`, [`setMaxLifecycle()`](https://developer.android.com/reference/androidx/fragment/app/FragmentTransaction?hl=zh-cn#setMaxLifecycle(androidx.fragment.app.Fragment,%20androidx.lifecycle.Lifecycle.State)) sets a maximum state for the given fragment. For example, [`ViewPager2`](https://developer.android.com/reference/androidx/viewpager2/widget/ViewPager2?hl=zh-cn) uses `setMaxLifecycle()` to limit the off-screen fragments to the `STARTED` state.

## Showing and hiding fragment's views

Use the `FragmentTransaction` methods [`show()`](https://developer.android.com/reference/androidx/fragment/app/FragmentTransaction?hl=zh-cn#show(androidx.fragment.app.Fragment)) and [`hide()`](https://developer.android.com/reference/androidx/fragment/app/FragmentTransaction?hl=zh-cn#hide(androidx.fragment.app.Fragment)) to show and hide the view of fragments that have been added to a container. These methods set the visibility of the fragment's views *without* affecting the lifecycle of the fragment.

## Attaching and detaching fragments

**Note:** The `attach()` and `detach()` methods are not related to the `Fragment` methods of [`onAttach()`](https://developer.android.com/reference/androidx/fragment/app/Fragment?hl=zh-cn#onAttach(android.content.Context)) and [`onDetach()`](https://developer.android.com/reference/androidx/fragment/app/Fragment?hl=zh-cn#onDetach()).
