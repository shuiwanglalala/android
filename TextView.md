# TextView

## [Autosizing TextViews](https://developer.android.com/guide/topics/ui/look-and-feel/autosizing-textview)

**If you set autosizing in an XML file, it is not recommended to use the value "wrap_content" for the layout_width or layout_height attributes of a TextView. It may produce unexpected results**

+ Default

  + The default dimensions for uniform scaling are minTextSize = 12sp, maxTextSize = 112sp, and granularity = 1px

+ Granularity

  + ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <TextView
        android:layout_width="match_parent"
        android:layout_height="200dp"
        android:autoSizeTextType="uniform"
        android:autoSizeMinTextSize="12sp"
        android:autoSizeMaxTextSize="100sp"
        android:autoSizeStepGranularity="2sp" />
    ```

+ Preset Sizes

# [Span](https://developer.android.com/guide/topics/text/spans#best-practices)

[Underspanding spans](https://medium.com/androiddevelopers/underspanding-spans-1b91008b97e4)

[android-spanned-spannedstring-spannable-spannablestring-and-charsequence](https://stackoverflow.com/questions/17546955/android-spanned-spannedstring-spannable-spannablestring-and-charsequence)