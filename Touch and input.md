# Touch and input

## 事件分发

## 点击注意事项

+ 点击区域放大

+ 点击互斥

  + recyclerview内，同时点击多个子item

+ 点击过滤

  + rxjava buffer

  + [onClick内直接过滤，但点击音效未被过滤](https://blog.csdn.net/zhufuing/article/details/53021835)

  + 点击后置disable，等待执行结束，重置enable

    + 等待时长不确定，体验不好；若无返回结果，造成无法点击

  + ```java
        public void enableClick(final boolean onClick) {
            mHandler.postDelayed(new Runnable() {
                @Override
                public void run() {
                    myView1.setClickable(onClick);
                    textView1.setClickable(onClick);
                }
            }, onClick ? 500 : 0);//点击事件间隔500ms
        }
        
        {
            enableClick(false);
            // 执行点击事件
            enableClick(true);
        }
    ```
