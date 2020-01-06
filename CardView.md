# CardView

[CardView](https://developer.android.com/reference/android/support/v7/widget/CardView)

A FrameLayout with a rounded corner background and shadow

Since padding is used to offset content for shadows, you cannot set padding on CardView. Instead, you can use content padding attributes in XML or `setContentPadding(int, int, int, int)` in code to set the padding between the edges of the CardView and children of CardView

To change CardView's elevation in a backward compatible way, use `setCardElevation(float)`

[Create a Card-Based Layout](https://developer.android.com/guide/topics/ui/layout/cardview)