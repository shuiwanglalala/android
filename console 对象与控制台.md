# console 对象与控制台

+ console 对象
+ console 对象的静态方法
  + console.log()，console.info()，console.debug()
    + console.log方法用于在控制台输出信息。它可以接受一个或多个参数，将它们连接起来输出
    + 第一个参数是格式字符串（使用了格式占位符），console.log方法将依次用后面的参数替换占位符，然后再进行输出
  + console.warn()，console.error()
  + console.table()
    + 对于某些复合类型的数据，console.table方法可以将其转为表格显示
  + console.count()
    + 用于计数，输出它被调用了多少次
    + 该方法可以接受一个字符串作为参数，作为标签，对执行次数进行分类
  + console.dir()，console.dirxml()
    + dir方法用来对一个对象进行检查（inspect），并以易于阅读和打印的格式显示
  + console.assert()
  + console.time()，console.timeEnd()
    + 这两个方法用于计时，可以算出一个操作所花费的准确时间
  + console.group()，console.groupEnd()，console.groupCollapsed()
  + console.trace()，console.clear()
    + console.trace方法显示当前执行的代码在堆栈中的调用路径
+ 控制台命令行 API
  + keys(object)方法返回一个数组，包含object的所有键名
  + values(object)方法返回一个数组，包含object的所有键值
+ debugger 语句
  + debugger语句主要用于除错，作用是设置断点。如果有正在运行的除错工具，程序运行到debugger语句时会自动停下。如果没有除错工具，debugger语句不会产生任何结果，JavaScript 引擎自动跳过这一句
  + Chrome 浏览器中，当代码运行到debugger语句时，就会暂停运行，自动打开脚本源码界面