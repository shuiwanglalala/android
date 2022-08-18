# 创建Fragment

## Add a fragment to an activity

It is strongly recommended to always use a `FragmentContainerView` as the container for fragments, as `FragmentContainerView` includes fixes specific to fragments that other view groups such as `FrameLayout` do not provide.

### Add a fragment via XML

The `android:name` attribute specifies the class name of the `Fragment` to instantiate. When the activity's layout is inflated, the specified fragment is instantiated, [`onInflate()`](https://developer.android.com/reference/androidx/fragment/app/Fragment?hl=zh-cn#onInflate(android.content.Context,%2520android.util.AttributeSet,%2520android.os.Bundle)) is called on the newly instantiated fragment, and a `FragmentTransaction` is created to add the fragment to the `FragmentManager`.

### Add a fragment programmatically

**Note:** You should **always** use `setReorderingAllowed(true)` when performing a `FragmentTransaction`

In the previous example, note that the fragment transaction is only created when `savedInstanceState` is `null`. This is to ensure that the fragment is added only once, when the activity is first created. When a configuration change occurs and the activity is recreated, `savedInstanceState` is no longer `null`, and the fragment does not need to be added a second time, as the fragment is automatically restored from the `savedInstanceState`.
