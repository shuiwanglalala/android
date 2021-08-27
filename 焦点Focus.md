# 焦点Focus

[TV端开发之焦点处理](https://lx8421bcd.github.io/2018/12/10/TV%E7%AB%AF%E5%BC%80%E5%8F%91%E4%B9%8B%E7%84%A6%E7%82%B9%E5%A4%84%E7%90%86/)

## 几个关于焦点的知识点

### 焦点数量

界面上的焦点数永远小于等于1，也就是说任何时候多最多只会有一个焦点，或者由于焦点丢失等因素界面上没有焦点

### View能否获取焦点

并不是所有View都默认能获取焦点，特别是随系统版本不同，View默认能否获取焦点也不一样，所以最好的做法是对于能获取焦点的View，在定义时设置`android:focusable:"true"`或`setFocusable(true)`

### has & is

`hasFocus()` 方法只要ViewGroup本身有焦点或其child有焦点都返回true，而 `isFocused()` 只有ViwGroup自身有焦点才返回true。同理还有 `isFocusable()` 和 `hasFocusable()` ，“is”判断自身，“has”判断自身和child

[View 的焦点机制](http://liwenkun.me/2018/04/06/android-focus/)

大概了解一下，不用太细节