android组件化

android 面向切换编程

arouter 获取fragment有什么意义

https://github.com/liu-xiao-dong/JD-Test



+ DialogFragment dialog popupwindow 框架 Utils内是否有dialog框架 dialog theme
+ dialog的各自子类
+ 您应避免直接实例化 Dialog

整理所有的dialog，考虑通用的对话框放置在common模块内

删除不再使用的dialog 的xml layout

guava

客厅推荐页无网络下无法刷新

星权益的ui

cardactivity banner图片变形

card缓存的有效期和有效性


showFileChooserWithRequestCode


webview 使用 封装 架构 性能 内存泄漏 页面回退

WebChromeClient

升级banner控件

OssService

遇到支付dialog后，再统一使用

京东 微信签约后，状态无法更新

引入流式布局

小程序在哪里

数据绑定更新list，如果只更新list中item的字段，如何更新ui呢



mass

+ 附近站点 线路详情 线路列表
+ 我的关注 搜索线路
+ 切换北京 广州公交
+ 

LocationUtils

CoordinateTransformUtil

运行时动态确认权限

首页fragment进入后需要登录判断

所有搜索sdk数据时的加载动画

+ 请求的错乱
  + 两个请求的判断和取消 防止数据错误
  + route 百度sdk请求和我们后台请求的冲突问题 不对应问题
+ 点击的错乱
  + 多个搜索item被同时点击的过滤
  + 一个item点击后，再点击第二个item，取消第一个item的订阅
  + 点击间隔放长一点
  + 多点item同时点击
  + 快速点击过滤



+ 搜索
  + 搜索结果为空的ui
  + 搜索结果列表 去线路规划 先显示10个
  + 点击 busStation
    + 完成了一点点
  + 地铁线路 道路 提供图标

+ poiinfo
  + 地图移动后需要复归
  + 地铁线路 公交线路 隐藏route按钮

+ roure plan
  + 执行新的线路规划前，清空之前的数据
  + 搜索结果为空的ui
  + 过滤无效的规划line
  + 没有时间设置
  + 切换的deounce延迟
  + 不更改node，进入搜索再回来，重新查了一遍
  + 下拉刷新