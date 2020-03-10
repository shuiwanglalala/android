# null, undefined 和布尔值

+ null 和 undefined
  + 概述
  + 用法和含义
+ 布尔值
  + 如果 JavaScript 预期某个位置应该是布尔值，会将该位置上现有的值自动转为布尔值。转换规则是除了下面六个值被转为false，其他值都视为true
    + undefined
    + null
    + false
    + 0
    + NaN
    + ""或''（空字符串）
  + 注意，空数组（[]）和空对象（{}）对应的布尔值，都是true
  + java kotlin中预期某个位置应该是布尔值，但实际为非布尔值，则不能通过编译