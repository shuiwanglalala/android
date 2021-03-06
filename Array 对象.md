# Array 对象

+ 构造函数
  + Array构造函数有一个很大的缺陷，就是不同的参数，会导致它的行为不一致。因此，不建议使用它生成新数组，直接使用数组字面量是更好的做法
+ 静态方法
  + Array.isArray()
    + Array.isArray方法返回一个布尔值，表示参数是否为数组。它可以弥补typeof运算符的不足
+ 实例方法
  + valueOf()，toString()
    + valueOf方法是一个所有对象都拥有的方法，表示对该对象求值。不同对象的valueOf方法不尽一致，数组的valueOf方法返回数组本身
    + toString方法也是对象的通用方法，数组的toString方法返回数组的字符串形式
  + **push()，pop()**
    + push方法用于在数组的末端添加一个或多个元素，并返回添加新元素后的数组长度。注意，该方法会改变原数组
    + pop方法用于删除数组的最后一个元素，并返回该元素。注意，该方法会改变原数组
      + push和pop结合使用，就构成了“后进先出”的栈结构（stack）
  + **shift()，unshift()**
    + shift()方法用于删除数组的第一个元素，并返回该元素。注意，该方法会改变原数组
      + push()和shift()结合使用，就构成了“先进先出”的队列结构（queue）
    + unshift()方法用于在数组的第一个位置添加元素，并返回添加新元素后的数组长度。注意，该方法会改变原数组
  + join()
    + join()方法以指定参数作为分隔符，将所有数组成员连接为一个字符串返回。如果不提供参数，默认用逗号分隔
  + concat()
    + 如果数组成员包括对象，concat方法返回当前数组的一个浅拷贝。所谓“浅拷贝”，指的是新数组拷贝的是对象的引用
  + **reverse()**
    + reverse方法用于颠倒排列数组元素，返回改变后的数组。注意，该方法将改变原数组
  + slice()
    + slice方法用于提取目标数组的一部分，返回一个新数组，原数组不变
    + 它的第一个参数为起始位置（从0开始），第二个参数为终止位置（但该位置的元素本身不包括在内）。如果省略第二个参数，则一直返回到原数组的最后一个成员
    + slice方法的一个重要应用，是将类似数组的对象转为真正的数组
  + **splice()**
    + splice方法用于删除原数组的一部分成员，并可以在删除的位置添加新的数组成员，返回值是被删除的元素。注意，该方法会改变原数组
    + 如果只是单纯地插入元素，splice方法的第二个参数可以设为0
    + 如果只提供第一个参数，等同于将原数组在指定位置拆分成两个数组
  + **sort()**
    + sort方法对数组成员进行排序，默认是按照字典顺序排序。排序后，原数组将被改变
    + 如果想让sort方法按照自定义方式排序，可以传入一个函数作为参数
      + 注意，自定义的排序函数应该返回数值，否则不同的浏览器可能有不同的实现，不能保证结果都一致
  + map()
    + map方法将数组的所有成员依次传入参数函数，然后把每一次的执行结果组成一个新数组返回
    + map方法接受一个函数作为参数。该函数调用时，map方法向它传入三个参数：当前成员、当前位置和数组本身
    + map方法还可以接受第二个参数，用来绑定回调函数内部的this变量
  + forEach()
    + forEach方法与map方法很相似，也是对数组的所有成员依次执行参数函数。但是，forEach方法不返回值，只用来操作数据。这就是说，如果数组遍历的目的是为了得到返回值，那么使用map方法，否则使用forEach方法
    + 注意，forEach方法无法中断执行，总是会将所有成员遍历完。如果希望符合某种条件时，就中断遍历，要使用for循环
  + filter()
    + 它的参数是一个函数，所有数组成员依次执行该函数，返回结果为true的成员组成一个新数组返回。该方法不会改变原数组
  + some()，every()
    + 这两个方法类似“断言”（assert），返回一个布尔值，表示判断数组成员是否符合某种条件
  + reduce()，reduceRight()
    + reduce方法和reduceRight方法依次处理数组的每个成员，最终累计为一个值。它们的差别是，reduce是从左到右处理（从第一个成员到最后一个成员），reduceRight则是从右到左（从最后一个成员到第一个成员），其他完全一样
  + indexOf()，lastIndexOf()
  + 链式使用