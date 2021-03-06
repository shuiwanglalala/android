# Java

+ Map
  + HashMap
    + 它根据键的hashCode值存储数据，大多数情况下可以直接定位到它的值，因而具有很快的访问速度，但遍历顺序却是不确定的。 HashMap最多只允许一条记录的键为null，允许多条记录的值为null。HashMap非线程安全，如果需要满足线程安全，可以用 Collections的synchronizedMap方法使HashMap具有线程安全的能力，或者使用ConcurrentHashMap
  + Hashtable
    + Hashtable不建议在新代码中使用，不需要线程安全的场合可以用HashMap替换，需要线程安全的场合可以用ConcurrentHashMap替换
  + LinkedHashMap
    + LinkedHashMap是HashMap的一个子类，保存了记录的插入顺序，在用Iterator遍历LinkedHashMap时，先得到的记录肯定是先插入的，也可以在构造时带参数，按照访问次序排序
  + TreeMap
    + TreeMap实现SortedMap接口，能够把它保存的记录根据键排序，默认是按键值的升序排序，也可以指定排序的比较器
    + 在使用TreeMap时，key必须实现Comparable接口或者在构造TreeMap传入自定义的Comparator，否则会在运行时抛出java.lang.ClassCastException类型的异常
  + 对于上述四种Map类型的类，要求映射中的key是不可变对象。不可变对象是该对象在创建后它的哈希值不会被改变

+ HashMap
  + 存储结构
    + 从结构实现来讲，HashMap是数组+链表+红黑树（JDK1.8增加了红黑树部分）实现的
    + Node是HashMap的一个内部类，实现了Map.Entry接口，本质就是一个映射(键值对)
    + HashMap就是使用哈希表来存储的。哈希表为解决冲突，可以采用开放地址法和链地址法等来解决问题，Java中HashMap采用了链地址法。链地址法，简单来说，就是数组加链表的结合。在每个数组元素上都一个链表结构，当数据被Hash后，得到数组下标，把数据放在对应下标元素的链表上
    + 如果哈希桶数组很大，即使较差的Hash算法也会比较分散，如果哈希桶数组数组很小，即使好的Hash算法也会出现较多碰撞，所以就需要在空间成本和时间成本之间权衡，其实就是在根据实际情况确定哈希桶数组（Node[] table）的大小，并在此基础上设计好的hash算法减少Hash碰撞。所以好的Hash算法和扩容机制至关重要
  + 扩容是一个特别耗性能的操作，所以使用HashMap的时候，估算map的大小，初始化的时候给一个大致的数值，避免map进行频繁的扩容
  + JDK1.8引入红黑树大程度优化了HashMap的性能，这主要体现在hash算法不均匀时，即产生的链表非常长，这时把链表转为红黑树可以将复杂度从O(n)降到O(logn)
  + HashMap是如何工作的？面试时可以这么回答：
    HashMap在Map.Entry静态内部类实现中存储key-value对。HashMap使用哈希算法，在put和get方法中，它使用hashCode()和equals()方法。当我们通过传递key-value对调用put方法的时候，HashMap使用Key hashCode()和哈希算法来找出存储key-value对的索引。Entry存储在LinkedList中，所以如果存在entry，它使用equals()方法来检查传递的key是否已经存在，如果存在，它会覆盖value，如果不存在，它会创建一个新的entry然后保存。当我们通过传递key调用get方法时，它再次使用hashCode()来找到数组中的索引，然后使用equals()方法找出正确的Entry，然后返回它的值
  + HashMap的查找时间复杂度只有在最理想的情况下才会为O(1)，而要保证这个理想状态不是我们开发者控制的

+ java内存管理
  + JVM内存空间管理
    + 方法区
      + 所有线程共享
      + 方法区存放了要加载的类的信息(如类名，修饰符)、类中的静态变量、final定义的常量、类中的field、方法信息
      + 在Hotspot虚拟机中，这块区域对应的是Permanent Generation(持久代)，一般的，方法区上执行的垃圾收集是很少的，因此方法区又被称为持久代的原因之一，但这也不代表着在方法区上完全没有垃圾收集
      + 运行时常量池（Runtime Constant Pool）是方法区的一部分，用于存储编译期就生成的字面常量、符号引用、翻译出来的直接引用（符号引用就是编码是用字符串表示某个变量、接口的位置，直接引用就是根据符号引用翻译出来的地址，将在类链接阶段完成翻译）；运行时常量池除了存储编译期常量外，也可以存储在运行时间产生的常量
    + 堆区
      + 所有线程共享
      + 在JVM所管理的内存中，堆区是最大的一块，堆区也是JavaGC机制所管理的主要内存区域。堆区用来存储对象实例及数组值，可以认为java中所有通过new创建的对象都在此分配
      + 年轻代（Young Generation）
        + 对象在被创建时，内存首先是在年轻代进行分配（注意，大对象可以直接在老年代分配）。当年轻代需要回收时会触发Minor GC(也称作Young GC)
        + 组成
          + Eden Space
            + 年轻代的Eden区内存是连续的，所以其分配会非常快；同样Eden区的回收也非常快
          + S0
            + 两块相同大小的Survivor Space（又称S0和S1）
          + S1
      + 老年代（Old Generation）
        + 老年代用于存放在年轻代中经多次垃圾回收仍然存活的对象，可以理解为比较老一点的对象，例如缓存对象；新建的对象也有可能在老年代上直接分配内存，这主要有两种情况：一种为大对象；另一种为大的数组对象
    + 本地方法栈
      + 支持native方法的执行，存储了每个native方法调用的状态。本地方法栈和虚拟机方法栈运行机制一致，它们唯一的区别就是，虚拟机栈是执行Java方法的，而本地方法栈是用来执行native方法的
    + 虚拟机栈
      + 虚拟机栈占用的是操作系统内存，每个线程都对应着一个虚拟机栈，它是线程私有的，而且分配非常高效。一个线程的每个方法在执行的同时，都会创建一个栈帧（Statck Frame），栈帧中存储的有局部变量表、操作站、动态链接、方法出口等，当方法被调用时，栈帧在JVM栈中入栈，当方法执行完成时，栈帧出栈
    + 程序计数器 
      + 个比较小的内存区域，可能是CPU寄存器或者操作系统内存，其主要用于指示当前线程所执行的字节码执行到了第几行，可以理解为是当前线程的行号指示器
  + 内存的回收方式
    + JVM通过GC来回收堆和方法区中的内存
    + 引用计数收集器
      + 引用计数器采用分散式管理方式，通过计数器记录对象是否被引用。当计数器为0时，说明此对象已经不再被使用，可进行回收
      + 引用计数器需要在每次对象赋值时进行引用计数器的增减，他有一定消耗。另外，引用计数器对于循环引用的场景没有办法实现回收
    + 跟踪收集器
      + 复制（Copying）
        + 复制采用的方式为从根集合扫描出存活的对象，并将找到的存活的对象复制到一块新的完全未被使用的空间中
      + 标记-清除（Mark-Sweep）
        + 标记-清除采用的方式为从根集合开始扫描，对存活的对象进行标记，标记完毕后，再扫描整个空间中未标记的对象，并进行清除
        + 标记-清除动作不需要进行对象移动，且仅对其不存活的对象进行处理。在空间中存活对象较多的情况下较为高效，但由于标记-清除直接回收不存活对象占用的内存，因此会造成内存碎片
      + 标记-压缩（Mark-Compact）
        + 标记-压缩和标记-清除一样，是对活的对象进行标记，但是在清除后的处理不一样，标记-压缩在清除对象占用的内存后，会把所有活的对象向左端空闲空间移动，然后再更新引用其对象的指针
        + 很明显，标记-压缩在标记-清除的基础上对存活的对象进行了移动规整动作，解决了内存碎片问题，得到更多连续的内存空间以提高分配效率，但由于需要对对象进行移动，因此成本也比较高

+ CLass类型信息

  + [Class类](https://www.liaoxuefeng.com/wiki/1252599548343744/1264799402020448)

    + 每加载一种class，JVM就为其创建一个Class类型的实例，并关联起来。这个Class实例是JVM内部创建的，如果我们查看JDK源码，可以发现Class类的构造方法是private，只有JVM能创建Class实例，我们自己的Java程序是无法创建Class实例的

      由于JVM为每个加载的class创建了对应的Class实例，并在实例中保存了该class的所有信息，包括类名、包名、父类、实现的接口、所有方法、字段等，因此，如果获取了某个Class实例，我们就可以通过这个Class实例获取到该实例对应的class的所有信息

      这种通过Class实例获取class信息的方法称为反射（Reflection）

      如果获取到了一个Class实例，我们就可以通过该Class实例来创建对应类型的实例。通过Class.newInstance()可以创建类实例，它的局限是：只能调用public的无参数构造方法。带参数的构造方法，或者非public的构造方法都无法通过Class.newInstance()被调用

      + 动态加载
        + JVM在执行Java程序的时候，并不是一次性把所有用到的class全部加载到内存，而是第一次需要用到class时才加载
        + 动态加载class的特性对于Java程序非常重要。利用JVM动态加载class的特性，我们才能在运行期根据条件加载不同的实现类

  + 访问字段

    + api
      + Field getField(name)：根据字段名获取某个public的field（包括父类）
      + Field getDeclaredField(name)：根据字段名获取当前类的某个field（不包括父类）
      + Field[] getFields()：获取所有public的field（包括父类）
      + Field[] getDeclaredFields()：获取当前类的所有field（不包括父类）
    + 一个Field对象包含了一个字段的所有信息
      + getName()：返回字段名称，例如，"name"
      + getType()：返回字段类型，也是一个Class实例，例如，String.class
      + getModifiers()：返回字段的修饰符，它是一个int，不同的bit表示不同的含义
      + 用Field.get(Object)获取指定实例的指定字段的值
        + 调用Field.setAccessible(true)的意思是，别管这个字段是不是public，一律允许访问
        + 此外，setAccessible(true)可能会失败。如果JVM运行期存在SecurityManager，那么它会根据规则进行检查，有可能阻止setAccessible(true)。例如，某个SecurityManager可能不允许对java和javax开头的package的类调用setAccessible(true)，这样可以保证JVM核心库的安全
      + 设置字段值是通过Field.set(Object, Object)实现的，其中第一个Object参数是指定的实例，第二个Object参数是待修改的值

  + 调用方法

    + api
      + Method getMethod(name, Class...)：获取某个public的Method（包括父类）
      + Method getDeclaredMethod(name, Class...)：获取当前类的某个Method（不包括父类）
      + Method[] getMethods()：获取所有public的Method（包括父类）
      + Method[] getDeclaredMethods()：获取当前类的所有Method（不包括父类）
    + 一个Method对象包含一个方法的所有信息
      + getName()：返回方法名称，例如："getScore"
      + getReturnType()：返回方法返回值类型，也是一个Class实例，例如：String.class
      + getParameterTypes()：返回方法的参数类型，是一个Class数组，例如：{String.class, int.class}
      + getModifiers()：返回方法的修饰符，它是一个int，不同的bit表示不同的含义
      + 对Method实例调用invoke就相当于调用该方法，invoke的第一个参数是对象实例，即在哪个实例上调用该方法，后面的可变参数要与方法参数一致，否则将报错
        + 为了调用非public方法，我们通过Method.setAccessible(true)允许其调用
        + 此外，setAccessible(true)可能会失败。如果JVM运行期存在SecurityManager，那么它会根据规则进行检查，有可能阻止setAccessible(true)。例如，某个SecurityManager可能不允许对java和javax开头的package的类调用setAccessible(true)，这样可以保证JVM核心库的安全
      + 如果获取到的Method表示一个静态方法，调用静态方法时，由于无需指定实例对象，所以invoke方法传入的第一个参数永远为null
    + 使用反射调用方法时，仍然遵循多态原则：即总是调用实际类型的覆写方法（如果存在）

  + 调用构造方法

    + api
      + getConstructor(Class...)：获取某个public的Constructor
      + getDeclaredConstructor(Class...)：获取某个Constructor
      + getConstructors()：获取所有public的Constructor
      + getDeclaredConstructors()：获取所有Constructor

  + 动态代理

    + 我们仍然先定义了接口Hello，但是我们并不去编写实现类，而是直接通过JDK提供的一个Proxy.newProxyInstance()创建了一个Hello接口对象。这种没有实现类但是在运行期动态创建了一个接口对象的方式，我们称为动态代码。JDK提供的动态创建接口对象的方式，就叫动态代理
    + 方式
      + 定义一个InvocationHandler实例，它负责实现接口的方法调用
      + 通过Proxy.newProxyInstance()创建interface实例，它需要3个参数
        + 使用的ClassLoader，通常就是接口类的ClassLoader
        + 需要实现的接口数组，至少需要传入一个接口进去
        + 用来处理接口方法调用的InvocationHandler实例
      + 将返回的Object强制转型为接口
    + [Java动态代理](https://juejin.im/post/5ad3e6b36fb9a028ba1fee6a)