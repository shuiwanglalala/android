# App Startup

## Initialize components at app startup

### Set up manifest entries

This means that in order for a component initializer to be discoverable by App Startup, one of the following conditions must be met

- The component initializer has a corresponding `` entry under the `InitializationProvider` manifest entry
- The component initializer is listed in the `dependencies()` method from an initializer that is already discoverable

## Manually initialize components

### Disable automatic initialization for an individual component

You use `tools:node="remove"` in the entry instead of simply removing the entry in order to make sure that the merger tool also removes the entry from all other merged manifest files

**Note:** Disabling automatic initialization for a component also disables automatic initialization for that component's dependencies





[App Startup 实践以及原理分析](https://juejin.im/post/5ee4bbe4f265da76b559bdfe)

有demo

[Jetpack新成员，App Startup一篇就懂](https://blog.csdn.net/guolin_blog/article/details/108026357)

[Android 启动优化（七） - JetPack App Startup 使用及源码浅析](https://juejin.cn/post/6952659008733839390)

[我为何弃用Jetpack的App Startup?](https://juejin.cn/post/6859500445669752846)