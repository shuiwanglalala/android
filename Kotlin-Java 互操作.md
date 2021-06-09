# Kotlin-Java 互操作

## Java（供 Kotlin 使用）

### 不得使用硬关键字

请勿将 Kotlin 的任何[硬关键字](https://kotlinlang.org/docs/reference/keyword-reference.html#hard-keywords)用作方法或字段的名称。从 Kotlin 调用时，这些硬关键字需要使用反引号进行转义。允许使用[软关键字](https://kotlinlang.org/docs/reference/keyword-reference.html#soft-keywords)、[修饰符关键字](https://kotlinlang.org/docs/reference/keyword-reference.html#modifier-keywords)和[特殊标识符](https://kotlinlang.org/docs/reference/keyword-reference.html#special-identifiers)

## Kotlin（供 Java 使用）

### 文件名

当文件包含顶级函数或属性时，应始终使用 `@file:JvmName("Foo")` 对其进行注释，以提供一个合适的名称

默认情况下，MyClass.kt 文件中的顶级成员最终会进入一个名为 `MyClassKt` 的类中，此名称没有吸引力，并且会泄露作为实现细节的语言

不妨考虑添加 `@file:JvmMultifileClass`，以将多个文件中的顶级成员组合到一个类中

### Lambda 参数

需要从 Java 中使用的[函数类型](https://kotlinlang.org/docs/reference/lambdas.html#function-types)应避免返回类型 `Unit`。这样做要求指定明确的 `return Unit.INSTANCE;` 语句，但该语句不符合语言习惯

在 Kotlin 中为 lambda 类型定义命名的单一抽象方法 (SAM) 接口可以为 Java 更正此问题，但这样就无法在 Kotlin 中使用 lambda 语法

要定义一个在 Java 和 Kotlin 中用作 lambda 的参数类型，又要求在这两种语言中使用时都感觉其符合语言习惯，这在目前还无法做到。当前的建议是优先选用函数类型，虽然当返回类型为 `Unit` 时在 Java 中的体验会受到影响

### 避免使用 `Nothing` 类属

类属参数为 `Nothing` 的类型会作为原始类型提供给 Java。原始类型在 Java 中很少使用，应避免使用

### 伴生函数

**伴生对象**中的公共函数必须带有 `@JvmStatic` 注释才能作为静态方法公开

如果没有该注释，则这些函数只能作为静态 `Companion` 字段中的实例方法使用

### 伴生常量

在 `companion object` 中作为有效常量的公共非 `const` 属性必须带有 `@JvmField` 注释才能作为静态字段公开

如果没有该注释，则这些属性只能作为静态 `Companion` 字段中命名奇怪的“getter”实例使用。使用 `@JvmStatic` 而不是 `@JvmField` 可将命名奇怪的“getter”移至类的静态方法，但这样仍然不正确

### 默认值的函数过载

参数具有默认值的函数必须使用 `@JvmOverloads`。如果没有此注释，则无法使用任何默认值来调用函数

使用 `@JvmOverloads` 时，应检查生成的方法，以确保它们每个都有意义。如果它们没有意义，请执行以下一种或两种重构，直到满意为止：

- 更改参数顺序，使具有默认值的参数尽量接近末尾
- 将默认值移至手动函数过载