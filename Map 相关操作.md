# Map 相关操作

## 取键与值

要从 Map 中检索值，必须提供其键作为 [`get()`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/-map/get.html) 函数的参数。 还支持简写 `[key]` 语法。 如果找不到给定的键，则返回 `null` 。 还有一个函数 [`getValue()`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/get-value.html) ，它的行为略有不同：如果在 Map 中找不到键，则抛出异常。 此外，还有两个选项可以解决键缺失的问题：

- [`getOrElse()`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/get-or-else.html) 与 list 的工作方式相同：对于不存在的键，其值由给定的 lambda 表达式返回
- [`getOrDefault()`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/get-or-default.html) 如果找不到键，则返回指定的默认值

要对 map 的所有键或所有值执行操作，可以从属性 `keys` 和 `values` 中相应地检索它们。 `keys` 是 Map 中所有键的集合， `values` 是 Map 中所有值的集合

## 过滤

可以使用 [`filter()`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/filter.html) 函数来[过滤](https://www.kotlincn.net/docs/reference/collection-filtering.html) map 或其他集合。 对 map 使用 `filter()` 函数时， `Pair` 将作为参数的谓词传递给它。 它将使用谓词同时过滤其中的键和值

还有两种用于过滤 map 的特定函数：按键或按值。 这两种方式，都有对应的函数： [`filterKeys()`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/filter-keys.html) 和 [`filterValues()`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/filter-values.html) 。 两者都将返回一个新 Map ，其中包含与给定谓词相匹配的条目。 `filterKeys()` 的谓词仅检查元素键， `filterValues()` 的谓词仅检查值

## `plus` 与 `minus` 操作

由于需要访问元素的键，[`plus`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/plus.html)（`+`）与 [`minus`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/minus.html)（`-`）运算符对 map 的作用与其他集合不同。 `plus` 返回包含两个操作数元素的 `Map` ：左侧的 Map 与右侧的 Pair 或另一个 Map 。 当右侧操作数中有左侧 `Map` 中已存在的键时，该条目将使用右侧的值

`minus` 将根据左侧 `Map` 条目创建一个新 `Map` ，右侧操作数带有键的条目将被剔除。 因此，右侧操作数可以是单个键或键的集合： list 、 set 等

## Map 写操作

Map 写操作的一些规则：

- 值可以更新。 反过来，键也永远不会改变：添加条目后，键是不变的
- 每个键都有一个与之关联的值。也可以添加和删除整个条目

### 添加与更新条目

要将新的键值对添加到可变 Map ，请使用 [`put()`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/-mutable-map/put.html) 。 将新条目放入 `LinkedHashMap` （Map的默认实现）后，会添加该条目，以便在 Map 迭代时排在最后。 在 Map 类中，新元素的位置由其键顺序定义

要一次添加多个条目，请使用 [`putAll()`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/put-all.html) 。它的参数可以是 `Map` 或一组 `Pair` ： `Iterable` 、 `Sequence` 或 `Array`

如果给定键已存在于 Map 中，则 `put()` 与 `putAll()` 都将覆盖值。 因此，可以使用它们来更新 Map 条目的值

还可以使用快速操作符将新条目添加到 Map 。 有两种方式：

- [`plusAssign`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/plus-assign.html) （`+=`） 操作符
- `[]` 操作符为 `set()` 的别名

### 删除条目

要从可变 Map 中删除条目，请使用 [`remove()`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/-mutable-map/remove.html) 函数。 调用 `remove()` 时，可以传递键或整个键值对。 如果同时指定键和值，则仅当键值都匹配时，才会删除此的元素

还可以通过键或值从可变 Map 中删除条目。 在 Map 的 `.keys` 或 `.values` 中调用 `remove()` 并提供键或值来删除条目。 在 `.values` 中调用时， `remove()` 仅删除给定值匹配到的的第一个条目

[`minusAssign`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/minus-assign.html) （`-=`） 操作符也可用于可变 Map