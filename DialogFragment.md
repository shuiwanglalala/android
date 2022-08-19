# DialogFragment

A [`DialogFragment`](https://developer.android.com/reference/androidx/fragment/app/DialogFragment?hl=zh-cn) is a special fragment subclass that is designed for creating and hosting [dialogs](https://developer.android.com/guide/topics/ui/dialogs?hl=zh-cn). Strictly speaking, you do not need to host your dialog within a fragment, but doing so allows the [`FragmentManager`](https://developer.android.com/guide/fragments/fragmentmanager?hl=zh-cn) to manage the state of the dialog and automatically restore the dialog when a configuration change occurs.

## Showing the `DialogFragment`

**Note:** Because the `DialogFragment` is automatically restored after configuration changes, consider only calling `show()` based on user actions or when `findFragmentByTag()` returns `null`, indicating that the dialog is not already present.

## `DialogFragment` lifecycle

Notice that you do not override [`onCreateView()`](https://developer.android.com/reference/androidx/fragment/app/Fragment?hl=zh-cn#oncreateview) or [`onViewCreated()`](https://developer.android.com/reference/androidx/fragment/app/Fragment?hl=zh-cn#onViewCreated(android.view.View,%20android.os.Bundle)) when using a `DialogFragment` with a `Dialog`. Dialogs are not only views—they have their own window. As such, it is insufficient to override `onCreateView()`. Moreover, `onViewCreated()` is never called on a custom `DialogFragment` unless you've overridden `onCreateView()` and provided a non-null view.

**Note:** When subscribing to lifecycle-aware components such as `LiveData`, you should never use [`viewLifecycleOwner`](https://developer.android.com/reference/androidx/fragment/app/Fragment?hl=zh-cn#getviewlifecycleowner) as the [LifecycleOwner](https://developer.android.com/reference/androidx/lifecycle/LifecycleOwner?hl=zh-cn) in a `DialogFragment` that uses `Dialog`s. Instead, use the `DialogFragment` itself, or if you're using [Jetpack Navigation](https://developer.android.com/guide/navigation?hl=zh-cn), use the [`NavBackStackEntry`](https://developer.android.com/reference/androidx/navigation/NavBackStackEntry?hl=zh-cn).

## Using custom views

You can create a `DialogFragment` and display a dialog by overriding [`onCreateView()`](https://developer.android.com/reference/androidx/fragment/app/Fragment?hl=zh-cn#onCreateView(android.view.LayoutInflater,%20android.view.ViewGroup,%20android.os.Bundle)), either giving it a `layoutId` as you would with a typical fragment or using the [`DialogFragment` constructor](https://developer.android.com/reference/androidx/fragment/app/DialogFragment?hl=zh-cn#DialogFragment(int)).

The `View` returned by [onCreateView()](https://developer.android.com/reference/androidx/fragment/app/Fragment?hl=zh-cn#onCreateView(android.view.LayoutInflater,%20android.view.ViewGroup,%20android.os.Bundle)) is automatically added to the dialog. In most cases, this means that you don't need to override [`onCreateDialog()`](https://developer.android.com/reference/androidx/fragment/app/DialogFragment?hl=zh-cn#onCreateDialog(android.os.Bundle)), as the default empty dialog is populated with your view.
