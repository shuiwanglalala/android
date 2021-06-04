# List 相关操作

## 按索引取元素

List 的特点是能通过索引访问特定元素，因此读取元素的最简单方法是按索引检索它。 这是通过 [`get()`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/-list/get.html) 函数或简写语法 `[index]` 来传递索引参数完成的

如果 List 长度小于指定的索引，则抛出异常。 另外，还有两个函数能避免此类异常：

- [`getOrElse()`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/get-or-else.html) 提供用于计算默认值的函数，如果集合中不存在索引，则返回默认值
- [`getOrNull()`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/get-or-null.html) 返回 `null` 作为默认值

## 取列表的一部分

除了[取集合的一部分](https://www.kotlincn.net/docs/reference/collection-parts.html)中常用的操作， List 还提供 [`subList()`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/-list/sub-list.html) 该函数将指定元素范围的视图作为列表返回。 因此，如果原始集合的元素发生变化，则它在先前创建的子列表中也会发生变化，反之亦然

## 查找元素位置

### 线性查找

在任何列表中，都可以使用 [`indexOf()`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/index-of.html) 或 [`lastIndexOf()`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/last-index-of.html) 函数找到元素的位置。 它们返回与列表中给定参数相等的元素的第一个或最后一个位置。 如果没有这样的元素，则两个函数均返回 `-1`

还有一对函数接受谓词并搜索与之匹配的元素：

- [`indexOfFirst()`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/index-of-first.html) 返回与谓词匹配的*第一个元素的索引*，如果没有此类元素，则返回 `-1`
- [`indexOfLast()`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/index-of-last.html) 返回与谓词匹配的*最后一个元素的索引*，如果没有此类元素，则返回 `-1`

### 在有序列表中二分查找

要搜索已排序列表中的元素，请调用 [`binarySearch()`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/binary-search.html) 函数，并将该值作为参数传递。 如果存在这样的元素，则函数返回其索引；否则，将返回 `(-insertionPoint - 1)`，其中 `insertionPoint` 为应插入此元素的索引，以便列表保持排序。 如果有多个具有给定值的元素，搜索则可以返回其任何索引

还可以指定要搜索的索引区间：在这种情况下，该函数仅在两个提供的索引之间搜索

#### Comparator 二分搜索？？

#### 比较函数二分搜索？？

## List 写操作

### 添加

要将元素添加到列表中的特定位置，请使用 [`add()`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/-mutable-list/add.html) 或 [`addAll()`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/add-all.html) 并提供元素插入的位置作为附加参数。 位置之后的所有元素都将向右移动

### 更新

列表还提供了在指定位置替换元素的函数——[`set()`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/-mutable-list/set.html) 及其操作符形式 `[]`。`set()` 不会更改其他元素的索引

[`fill()`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/fill.html) 简单地将所有集合元素的值替换为指定值

### 删除

要从列表中删除指定位置的元素，请使用 [`removeAt()`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/-mutable-list/remove-at.html) 函数，并将位置作为参数。 在元素被删除之后出现的所有元素索引将减 1

For removing the first and the last element, there are handy shortcuts [`removeFirst()`](https://www.kotlincn.net/api/latest/jvm/stdlib/kotlin.collections/-mutable-list/remove-first.html) and [`removeLast()`](https://www.kotlincn.net/api/latest/jvm/stdlib/kotlin.collections/-mutable-list/remove-last.html). Note that on empty lists, they throw an exception. To receive `null` instead, use [`removeFirstOrNull()`](https://www.kotlincn.net/api/latest/jvm/stdlib/kotlin.collections/-mutable-list/remove-first-or-null.html) and [`removeLastOrNull()`](https://www.kotlincn.net/api/latest/jvm/stdlib/kotlin.collections/-mutable-list/remove-last-or-null.html)