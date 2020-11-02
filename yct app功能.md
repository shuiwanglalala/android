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



XtcRechargeViewModel

LossReportPayAdapter

ChildrenCardPayAdapter

StudentCardApplyPayViewModel

NFCMainActivity



+ 重点测试部分
  + 卡充值页内支持招行支付（分已安装招行app和未安装招行app两种情况）
    + 测试选择卡号的弹窗是否正常，绑5张卡后查看弹窗是否正常滑动显示
  + 卡充值页内其他方式（羊城通宝/微信/支付宝）是否正常付款，切换支付渠道后是否正常
  + 免密支付列表/免密支付详情页，各类支付方式开通/关闭是否正常
    + 入口分三个：设置页/广州公交二维码页面/地铁二维码页。注意各类支付渠道开通/关闭后，对前面三个页面ui的影响
  + 微信支付成功/失败后，页面内通知及ui是否正常
  + 广州公交二维码页面，接入招行免密支付
    + 切换支付渠道后是否正常
    + 用户有欠费订单后，不支持二维码生成，点击支付进入招行欠费列表页，测试是否正常缴费，以及缴费成功后的列表ui变化

+ 简单过下功能

  + 5.9.1记名卡优化的部分

    