# Java泛型

https://www.bilibili.com/video/BV1xJ411n77R?p=1

https://blog.csdn.net/Beyondczn/article/details/107093693

[Java 泛型 <? super T> 中 super 怎么 理解？与 extends 有何不同？](https://www.zhihu.com/question/20400700)

Java 的泛型本身是不支持协变和逆变的

- 可以使用泛型通配符 `? extends` 来使泛型支持协变，但是「只能读取不能修改」，这里的修改仅指对泛型集合添加元素，如果是 `remove(int index)` 以及 `clear` 当然是可以的
- 可以使用泛型通配符 `? super` 来使泛型支持逆变，但是「只能修改不能读取」，这里说的不能读取是指不能按照泛型类型读取，你如果按照 `Object` 读出来再强转当然也是可以的