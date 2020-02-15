# Object 对象

+ 概述
  + JavaScript 的所有其他对象都继承自Object对象，即那些对象都是Object的实例
  + Object对象的原生方法分成两类：Object本身的方法与Object的实例方法
+ Object()
  + Object本身是一个函数，可以当作工具方法使用，将任意值转为对象。这个方法常用于保证某个值一定是对象
    + 如果参数为空（或者为undefined和null），Object()返回一个空对象
    + 如果参数是原始类型的值，Object方法将其转为对应的包装对象的实例
    + 如果Object方法的参数是一个对象，它总是返回该对象，即不用转换
      + 利用这一点，可以写一个判断变量是否为对象的函数
+ Object 构造函数
  + 通过var obj = new Object()的写法生成新对象，与字面量的写法var obj = {}是等价的。或者说，后者只是前者的一种简便写法
  + Object构造函数的用法与工具方法很相似，几乎一模一样。使用时，可以接受一个参数，如果该参数是一个对象，则直接返回这个对象；如果是一个原始类型的值，则返回该值对应的包装对象
  + 虽然用法相似，但是Object(value)与new Object(value)两者的语义是不同的，Object(value)表示将value转成一个对象，new Object(value)则表示新生成一个对象，它的值是value
+ Object 的静态方法
  + Object.keys()，Object.getOwnPropertyNames()
    + 对于一般的对象来说，Object.keys()和Object.getOwnPropertyNames()返回的结果是一样的。只有涉及不可枚举属性时，才会有不一样的结果。Object.keys方法只返回可枚举的属性（详见《对象属性的描述对象》一章），Object.getOwnPropertyNames方法还返回不可枚举的属性名
  + 其他方法
    + 对象属性模型的相关方法
      + Object.getOwnPropertyDescriptor()：获取某个属性的描述对象
      + Object.defineProperty()：通过描述对象，定义某个属性
      + Object.defineProperties()：通过描述对象，定义多个属性
    + 控制对象状态的方法
      + Object.preventExtensions()：防止对象扩展
      + Object.isExtensible()：判断对象是否可扩展
      + Object.seal()：禁止对象配置
      + Object.isSealed()：判断一个对象是否可配置
      + Object.freeze()：冻结一个对象
      + Object.isFrozen()：判断一个对象是否被冻结
    + 原型链相关方法
      - Object.create()：该方法可以指定原型对象和属性，返回一个新的对象。
      - Object.getPrototypeOf()：获取对象的Prototype对象。
+ Object 的实例方法
  + Object.prototype.valueOf()
    + valueOf方法的作用是返回一个对象的“值”，默认情况下返回对象本身
    + valueOf方法的主要用途是，JavaScript 自动类型转换时会默认调用这个方法
  + Object.prototype.toString()
    + toString方法的作用是返回一个对象的字符串形式，默认情况下返回类型字符串
  + toString() 的应用：判断数据类型
    + 由于实例对象可能会自定义toString方法，覆盖掉Object.prototype.toString方法，所以为了得到类型字符串，最好直接使用Object.prototype.toString方法。通过函数的call方法，可以在任意值上调用这个方法，帮助我们判断这个值的类型
      + 不同数据类型的Object.prototype.toString方法返回值如下
        + 数值：返回[object Number]
        + 字符串：返回[object String]
        + 布尔值：返回[object Boolean]
        + undefined：返回[object Undefined]
        + null：返回[object Null]
        + 数组：返回[object Array]
        + arguments 对象：返回[object Arguments]
        + 函数：返回[object Function]
        + Error 对象：返回[object Error]
        + Date 对象：返回[object Date]
        + RegExp 对象：返回[object RegExp]
        + 其他对象：返回[object Object]
  + Object.prototype.toLocaleString()
    + 这个方法的主要作用是留出一个接口，让各种不同的对象实现自己版本的toLocaleString，用来返回针对某些地域的特定的值
  + Object.prototype.hasOwnProperty()
    + Object.prototype.hasOwnProperty方法接受一个字符串作为参数，返回一个布尔值，表示该实例对象自身是否具有该属性