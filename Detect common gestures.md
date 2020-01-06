# Detect common gestures

## Detect gestures

[安卓自定义View进阶-手势检测(GestureDetector)](https://www.gcssloop.com/customview/gestruedector)

+ OnDoubleTapListener

  + onDoubleTap
    + onDoubleTap 在第二次手指按下(down)时触发
  + onSingleTapConfirmed
    + 如果你只想监听双击事件，那么只用关注 onDoubleTap 就行了，如果你同时要监听单击事件则需要关注 onSingleTapConfirmed 这个回调函数
  + onDoubleTapEvent
    + 在双击事件确定发生时会对第二次按下产生的 MotionEvent 信息进行回调
    + onDoubleTapEvent 是一种实时回调

+ OnGestureListener

  + onFling

    + Fling 中文直接翻译过来就是一扔、抛、甩，最常见的场景就是在 ListView 或者 RecyclerView 上快速滑动时手指抬起后它还会滚动一段时间才会停止。onFling 就是检测这种手势的

  + onShowPress

    + 它是用户按下时的一种回调，主要作用是给用户提供一种视觉反馈，可以在监听到这种事件时可以让控件换一种颜色，或者产生一些变化，告诉用户他的动作已经被识别。不过这个消息和 onSingleTapConfirmed 类似，也是一种延时回调，延迟时间是 180 ms，假如用户手指按下后立即抬起或者事件立即被拦截，时间没有超过 180 ms的话，这条消息会被 remove 掉，也就不会触发这个回调

  + onSingleTapUp

    + 和上面的 onSingleTapConfirmed 有不同，双击也被认为是一次onSingleTapUp

  + onScroll

    + onSrcoll 后两个参数不是速度，而是滚动的距离
