# 熟悉yct app使用和代码

## 主要tab

+ 引导页和启动页

+ 服务

  + 天气

  + banner 轮播 跳转-------BannerActivity

    + 最多6张

  + 横向tab栏

    需要登录

    + 充值中心

      跳转---------充值中心列表页 ReChargeCenterActivity

    + 学生卡

      跳转---------学生卡页 StudentCardMainActiivity

    + 旅游卡

      跳转----------广州城市旅游卡页

    + 羊城通商场

      跳转-----------羊城通商场首页 BrowserActivity

    + 领福利

      跳转---------------积分出行首页 BrowserActivity

  + 我的羊城通卡

    最多绑定5张卡

    卡的状态

    + 正常状态
    + 挂失状态
    + 未绑定卡状态

    + 需要登录
      + 我的羊城通页 RealNameCardFaceActivity
      + 添加卡片页 BindCardActivity
      + 账单-------------羊城通账单页 BrowserActivity

    

  + 羊城资讯

    不需要登录

    + 更多---------跳转至 羊城资讯列表页 LocalLifeActivity
    + item----------跳转至 羊城通资讯页 BrowserActivity

+ 社区

  点击顶栏tab，切换4个子页；横向滑动，顺序切换4个子页

  搜索子页需要登录，其余子页不需要

  整个页面有下拉刷新，刷新什么内容 代码内查看

  + 推荐

    +  公告

      自动轮询显示公告信息

      点击

      + 需要登录
  + 跳转至------公告消息页
    
  + 三个banner
  
      banner没有主动轮询替换

      + 母亲节-----跳转至 羊城说/感恩母亲
  + 致敬逆行者------跳转至 羊城说/致敬逆行者
      + 世界地球日-------跳转至 羊城说/出行账单
  
    + 热门
  
      item图片超过3张时，显示3张图片，否则只显示一张，或无图片就不显示

      item点击
  
      + 需要登录
    + 同时点击两个item会跳转2个内容详情页 bug
      + 跳转至---------内容详情页
      + 点赞
        + 不需要跳转--------内容详情页
        + 快速点击，点赞数会出现负数 bug
    
  + 线路说说
  
    + 公告

      与 推荐/公告 数据一致

      上下轮询显示公告内容

      点击

      + 需要登录
  + 跳转至------公告消息页
    
  + 推荐
  
      item点击
  
      + 需要登录
  + 跳转至--------XXX路说说 
      + 关注，不需要跳转------XXX路说说 
  
    + 关注
  
      去关注 需要登录
  
      item点击

      + 不再提示  已关注
+ 需要登录
      
    + 跳转至--------XXX路说说 
    
+ 羊城说
  
    + 顶栏类别tab
  
      点击tab切换各子标题的内容列表
  
      点击相同tab是重复刷新

    + 内容列表

      item

      + 点击需要网络
  + 跳转至---------内容详情页
      
    item排序，默认从时间上最新到最远
      
    top item需要满足什么条件  服务端
      
    + 跳转----------编辑话题页
  
  + 友爱车厢
  
    + 寻物启事
  
      点击item

      + 需要网络
    + 跳转至----------寻物启事列表页
      + 跳转至----------寻物启事详情页
    + 跳转至----------寻物启事发布页
  
  + 寻人启事
  
      点击item
      
      + 需要网络
    + 发布寻人启事
  
+ 搜索
  
    依据当前tab跳转至---------对应的搜索页
  
+ 生活

  第一次今天 生活 页面，有手势UI，用于提示用户小程序

+ 我的

## 子页面

+ BannerActivity

+ 羊城通资讯列表页 LocalLifeActivity

  item----------跳转羊城通资讯页 BrowserActivity

+ 充值中心列表页 ReChargeCenterActivity

  + 转账充值-------------转账充值页 TransforAccountActivity
  + NFC充值
  + 蓝牙充值------------蓝牙充值页 BluetoothScanActivity
  + 手机SIM卡充值

+ 转账充值页 TransferAccountActivity

  + 转账记录--------------充值记录页 CardRecordsActivity

  + 输入或选择卡号

  + 支付方式

    + 羊城通宝----------羊城通宝页 YctbAcctActivity

    + 微信

      必须安装微信，才能使用微信支付

    + 支付宝-------------登录支付宝页 H5PayActivity

+ 充值记录页 CardRecordsActivity

  **有充值记录的UI是怎么样的**

+ 交易记录页 CardRecordsActivity

  + item点击-----------交易详情页 CardTradeDetailActivity

+ 交易详情页 CardTradeDetailActivity

+ 登录支付宝页 H5PayActivity

+ 羊城通宝页 YctbAcctActivity

  + 明细--------------羊城通宝明细页 YctbBillListActivity
  + 充值--------------充值羊城通宝页 TctbInOutActivity
  + 退款------------羊城通宝申请退款页  TctbInOutActivity

+ 羊城通宝明细页 YctbBillListActivity

  **有记录的明细UI是怎么样的**

  + **类型的具体区别**
    + 羊城通卡
    + 商场
    + 交通票
    + 乘车码
    + 学生卡
    + 羊城通宝

+ 充值羊城通宝页 TctbInOutActivity
  + 支付方式
  + 充值金额
  + 充值
    + 必须安装微信，才能使用微信支付
    + 登录支付宝页 H5PayActivity

+ 羊城通宝申请退款页  TctbInOutActivity
  + 到帐帐号 **选择支付宝还是微信的依据？？**  没有微信

+ 蓝牙充值页 BluetoothScanActivity
  + **怎样蓝牙充值？？**

+ 学生卡页 StudentCardMainActiivity

  + 申办------------学生卡办理页 StudentCardCheckActivity

  + 挂失补办---------学生卡挂失 ContainerActivity

  + 续期

  + 申办记录

    **UI是怎么样的？？**

  + 补办记录

    **UI是怎么样的？？**

+ 学生卡办理页 StudentCardCheckActivity

  **身份证号非法**

+ 学生卡挂失 ContainerActivity
  + 选择申办学校----------选择学校页 selectSchoolActivity
  + 同意 补办须知

+ 选择学校页 selectSchoolActivity

+ 我的羊城通页 记名卡 RealNameCardFaceActivity

  **有多张卡，UI怎么显示？？**

  + 已绑定 记名卡
  + 设置昵称---------设置备注名页 CardNickNameActivity
  + 去充值------------充值中心列表页 ReChargeCenterActivity
  + 帐号余额 是指羊城通宝余额
  + **卡片状态有几种** 不止于 正常 挂失，还有其他状态
  + 交易记录--------交易记录页 CardRecordsActivity
  + 充值记录--------------充值记录页 CardRecordsActivity
  + **挂失怎么测？？**
  + **无法解除绑定？？**

+ 我的羊城通页 普通卡 UnRealNameCardFaceActivity

  **返回该页是UI会多出一项 升级为记名卡**

  + 已绑定 普通卡
  + 升级为记名卡
    + --------------实名认证图片页 RealNamePicActivity
    + --------------升级为记名卡页  UploadCardPicActivity
  + 若没有实名认证，则出现提问框，引导用户进行实名认证；实名认证后，处于 卡信息审核中-------------实名认证等待页 RealNameReviewActivity

+ 设置备注名页 CardNickNameActivity

  + 设置昵称
+ **设置空备注名也能成功？？**
    + **设置昵称无效？？**

+ 实名认证图片页 RealNamePicActivity
  + 拍摄/上传图片
    + 拍摄--------------拍摄页 RealNamePhotoCameraActivity
  + 隐私政策---------------隐私政策页 ProtocolDetailActivity
  + 下一步-----------实名认证页RealNameConfirmActivity

+ 拍摄页 RealNamePhotoCameraActivity
+ 隐私政策页 ProtocolDetailActivity
+ 实名认证页RealNameConfirmActivity
  + 确认--------------实名认证视频页RealNameVideoActivity
+ 实名认证视频页RealNameVideoActivity

+ 升级为记名卡页  UploadCardPicActivity

  需要上传图片成功后才能确认提交

  + 确认提交----------------设置服务密码页SetServicePswInNewProcActivity

+ 设置服务密码页SetServicePswInNewProcActivity
  + 实名认证协议----------升级记名卡协议 ProtocolDetailActivity
  + 确认提交--------------实名认证等待页 RealNameReviewActivity

+ 实名认证等待页 RealNameReviewActivity

+ 1
+ 添加卡片页 BindCardActivity
  + 立即绑定--------------我的羊城通页（普通/记名）











+ 公告消息页

  点击item-------------跳转至公告消息详情页

  每篇公告至多显示9张图片

  图片

  + 可点击放大显示
  + 多张图片可横向滑动切换

+ 公告消息详情页

  图片

  + 可点击放大显示
  + 多张图片可横向滑动切换

  **点击底部空白处，跳转空白图片页**

+ 内容详情页

  类似于 XXX路说说评价详情页

  + 图片
    + 可点击放大显示
    + 多张图片可横向滑动切换
  + 点赞
  + 添加评论

+ 编辑话题页

  没有依据标签的输入提示

  + 选择标签---------可以不选
  + 标题---------必须要有
  + 内容-------必须要有
  + 图片

+ XXX路说说

  + 车站路线图

    首尾站的左右顺序可以调整

  + 公告

    + **点击右侧箭头附近区域，崩溃了？**
  + 跳转至-------------公告消息详情页
    
  + 线路评价

    点击item--------跳转 XXX路说说评价详情页

    + 全部
      + 当前在 全部模块，再次点击 全部按钮，还出现刷新动画
    + 最新
    + 有图评价

  + 添加评价------跳转 XXX路说说评价添加页

+ XXX路说说评价详情页

  最多显示三个标签

  **自己还能举报自己？**

  + 点赞

  + 关注XXX路线

  + 对1级评价，可以写2级评价

    3级评价的显示，至多显示2条

    **2级评价和3级评价的关系，到底是怎么样的？**

    **评价可以一直嵌套**

    点击评价----------跳转至XXX路说说评价回复页
    
    举报---------跳转至XXX路说说评价举报页

+ XXX路说说评价回复页

+ XXX路说说评价举报页

  + 其他原因

    必须提供内容输入，才能举报

+ XXX路说说评价添加页

  进入该页面时，顶部被部分遮住  bug

  + 发表

    必须要填写了内容，才能发表

  + 线路评分

    只要评了分，就至少1颗心

  + 选择标签

    至多选择3个标签

    标签有记忆性，对应不同心数

  + 评论内容填写

  + 评论图片上传

    至多上传3张图片

+ 寻物启事列表页

  + 跳转至---------发布寻物启事页
  
+ 顶栏tab
  
+ 跳转至----------寻物启事详情页
  
+ 寻物启事详情页

  类似于 XXX路说说评价详情页

+ 寻物启事发布页

  + 标题

  + 失物类型

  + 遗失路线

    搜索路线

  + 遗失站点 

    表格形式选择站点

  + 遗失时间

  + 内容描述

  + 联系人

  + 联系电话

  + 同意免责声明

+ 搜索页

  貌似搜索跳转有点问题   是的

  点击进入才算有搜索记录

  + 线路搜索
  
+ 话题搜索
  
  + 寻人/物搜索



## svn pdf说明

22启动页_引导页-V2-20191224



21服务-3.0-V5

04转账充值__V2

03我的卡片（卡片管理）_V6-191223

15普通卡升级为记名卡-V6-20200225

26羊城通账单-V7-20190620



20社区-D-20181204

+ 线路说说内是否有消息通知  没有
+ 我的-已登录

20社区-规则说明-A2018112

+ B-0014
+ B-0016
+ 羊城说是否还有公告  没有了
+ 我的-已登录

20社区-使用流程图-B-20181126

31 社区2期-v4

46.社区3期优化-v2-20200401



## 其他问题和代办

+ 
+ **服务密码是和记名卡一一对应**
+ 代办
  + nfc功能的测试手机
  + 一张学生卡
  + sim卡支持充值