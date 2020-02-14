# Object 对象的相关方法

+ Object.getPrototypeOf()
  + Object.getPrototypeOf方法返回参数对象的原型。这是获取原型对象的标准方法
+ Object.setPrototypeOf()
  + Object.setPrototypeOf方法为参数对象设置原型，返回该参数对象。它接受两个参数，第一个是现有对象，第二个是原型对象
+ Object.create()
  + 该方法接受一个对象作为参数，然后以它为原型，返回一个实例对象。该实例完全继承原型对象的属性
  + 使用Object.create方法的时候，必须提供对象原型，即参数不能为空，或者不是对象，否则会报错
  + 除了对象的原型，Object.create方法还可以接受第二个参数。该参数是一个属性描述对象，它所描述的对象属性，会添加到实例对象，作为该对象自身的属性
+ Object.prototype.isPrototypeOf()
  + 实例对象的isPrototypeOf方法，用来判断该对象是否为参数对象的原型
+ Object.prototype.__proto__
  + 实例对象的__proto__属性（前后各两个下划线），返回该对象的原型。该属性可读写
  + 根据语言标准，__proto__属性只有浏览器才需要部署，其他环境可以没有这个属性。它前后的两根下划线，表明它本质是一个内部属性，不应该对使用者暴露。因此，应该尽量少用这个属性，而是用Object.getPrototypeOf()和Object.setPrototypeOf()，进行原型对象的读写操作
+ 获取原型对象方法的比较
  + 获取实例对象obj的原型对象，有三种方法

    + obj.__proto__
      + 只有浏览器才需要部署，其他环境可以不部署
    + obj.constructor.prototype
      + 在手动改变原型对象时，可能会失效
    + Object.getPrototypeOf(obj)
      + 推荐使用
+ Object.getOwnPropertyNames()
  + 返回一个数组，成员是参数对象本身的所有属性的键名，不包含继承的属性键名
    + Object.getOwnPropertyNames方法返回所有键名，不管是否可以遍历
  + 只获取那些可以遍历的属性，使用Object.keys方法
+ Object.prototype.hasOwnProperty()
  + hasOwnProperty方法是 JavaScript 之中唯一一个处理对象属性时，不会遍历原型链的方法
+ in 运算符和 for...in 循环
+ 对象的拷贝