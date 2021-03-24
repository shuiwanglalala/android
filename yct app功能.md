https://github.com/google/agera

google 编程范式

https://fblitho.com/

ui架构

https://github.com/JessYanCoding/AndroidAutoSize/blob/master/README-zh.md

guava



https://github.com/AppIntro/AppIntro

https://github.com/yangfuhai/ASimpleCache

https://github.com/JakeWharton/DiskLruCache

https://github.com/amitshekhariitbhu/Android-Debug-Database

https://github.com/markzhai/AndroidPerformanceMonitor





动画

https://github.com/nikhilpanju/FabFilter

https://github.com/airbnb/lottie-android

炸天的动画

https://github.com/facebook/shimmer-android



android组件化

android 面向切换编程

arouter 获取fragment有什么意义



OssService



+ 步行规划
+ 按图取点

主页fragment

+ 显示home

routeplan

+ 显示home

PoiInfoActivity

+ 显示是否已收藏 ui

NaviSearchActivity

+ 显示home



item 第一个的divider隐藏

广州资讯 第一个firstItem

news list 入口;

 home head banner 点击跳转；点击上报

分享 点赞



跳小程序

html第一次加载失败



sim充值需要测试



```
public void selectBusCode() {
        mViewPager.postDelayed(new Runnable() {
            @Override
            public void run() {
                mViewPager.setCurrentItem(POSITION_BUS, true);
                setTab(POSITION_BUS);
                if (getQrcodeContainerFragment().getCurrentCity().equals(GUANGZHOU)) {
                    mQRCodeContainer.getGuangzhouQRCodeFragment().checkHasJftCard(true);
                }
            }
        }, 200);
    }
```

subway qrcode 入口要改 ui要改

bus qrcode入口要改 ui要改



