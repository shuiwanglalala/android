# Creating a View Class

## Define Custom Attributes

The name of the styleable entity is, by convention, the same name as the name of the class that defines the custom view. Although it's not strictly necessary to follow this convention, many popular code editors depend on this naming convention to provide statement completion

Once you define the custom attributes, you can use them in layout XML files just like built-in attributes. The only difference is that your custom attributes belong to a different namespace. Instead of belonging to the `http://schemas.android.com/apk/res/android` namespace, they belong to `http://schemas.android.com/apk/res/[your package name]`

## Apply Custom Attributes

```java
public PieChart(Context context, AttributeSet attrs) {
   super(context, attrs);
   TypedArray a = context.getTheme().obtainStyledAttributes(
        attrs,
        R.styleable.PieChart,
        0, 0);

   try {
       mShowText = a.getBoolean(R.styleable.PieChart_showText, false);
       textPos = a.getInteger(R.styleable.PieChart_labelPosition, 0);
   } finally {
       a.recycle();
   }
}
```

## Add Properties and Events

```java
public boolean isShowText() {
   return mShowText;
}

public void setShowText(boolean showText) {
   mShowText = showText;
   invalidate();
   requestLayout();
}
```

A good rule to follow is to always expose any property that affects the visible appearance or behavior of your custom view

