# This表达式

为了表示当前的 *接收者* 我们使用 *this* 表达式

- 在[类](https://www.kotlincn.net/docs/reference/classes.html#继承)的成员中，*this* 指的是该类的当前对象
- 在[扩展函数](https://www.kotlincn.net/docs/reference/extensions.html)或者[带有接收者的函数字面值](https://www.kotlincn.net/docs/reference/lambdas.html#带有接收者的函数字面值)中， *this* 表示在点左侧传递的 *接收者* 参数

如果 *this* 没有限定符，它指的是最内层的包含它的作用域。要引用其他作用域中的 *this*，请使用 *标签限定符*

## 限定的 *this*

访问来自外部作用域的*this*（一个[类](https://www.kotlincn.net/docs/reference/classes.html) 或者[扩展函数](https://www.kotlincn.net/docs/reference/extensions.html)， 或者带标签的[带有接收者的函数字面值](https://www.kotlincn.net/docs/reference/lambdas.html#带有接收者的函数字面值)）我们使用`this@label`，其中 `@label` 是一个代指 *this* 来源的标签

## Implicit `this`

当对 `this` 调用成员函数时，可以省略 `this.` 部分。 但是如果有一个同名的非成员函数时，请谨慎使用，因为在某些情况下会调用同名的非成员