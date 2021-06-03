# Kotlin排序

定义一个 `Comparator` 的一种比较简短的方式是标准库中的 [`compareBy()`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.comparisons/compare-by.html) 函数。 `compareBy()` 接受一个 lambda 表达式，该表达式从一个实例产生一个 `Comparable` 值，并将自定义顺序定义为生成值的自然顺序

## 自然顺序

基本的函数 [`sorted()`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/sorted.html) 和 [`sortedDescending()`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/sorted-descending.html) 返回集合的元素，这些元素按照其自然顺序升序和降序排序。 这些函数适用于 `Comparable` 元素的集合

## 自定义顺序

为了按照自定义顺序排序或者对不可比较对象排序，可以使用函数 [`sortedBy()`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/sorted-by.html) 和 [`sortedByDescending()`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/sorted-by-descending.html)。 它们接受一个将集合元素映射为 `Comparable` 值的选择器函数，并以该值的自然顺序对集合排序

如需为集合排序定义自定义顺序，可以提供自己的 `Comparator`。 为此，调用传入 `Comparator` 的 [`sortedWith()`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/sorted-with.html) 函数

## 倒序

你可以使用 [`reversed()`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/reversed.html) 函数以相反的顺序检索集合

`reversed()` 返回带有元素副本的新集合。 因此，如果你之后改变了原始集合，这并不会影响先前获得的 `reversed()` 的结果

另一个反向函数——[`asReversed()`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/as-reversed.html)——返回相同集合实例的一个反向视图，因此，如果原始列表不会发生变化，那么它会比 `reversed()` 更轻量，更合适；如果原始列表是可变的，那么其所有更改都会反映在其反向视图中，反之亦然

## 随机顺序

最后，[`shuffled()`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/shuffled.html) 函数返回一个包含了以随机顺序排序的集合元素的新的 `List`。 你可以不带参数或者使用 [`Random`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.random/-random/index.html) 对象来调用它