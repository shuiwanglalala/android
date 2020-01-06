# mvp-dagger

[Dagger](https://dagger.dev/)

[轻松学，浅析依赖倒置（DIP）、控制反转(IOC)和依赖注入(DI)](https://blog.csdn.net/briblue/article/details/75093382)

+ 依赖倒置 (Dependency inversion principle)
  + 上层模块不应该依赖底层模块，它们都应该依赖于抽象
  + 抽象不应该依赖于细节，细节应该依赖于抽象
+ 控制反转 （IoC）
  + IoC 模式最核心的地方就是在于依赖方与被依赖方之间，也就是上文中说的上层模块与底层模块之间引入了第三方，这个第三方统称为 IoC 容器，因为 IoC 容器的介入，导致上层模块对于它的依赖的实例化控制权发生变化，也就是所谓的控制反转的意思
+ 依赖注入（Dependency injection）
  + 一种实现 IoC 的手段
  + 我不想自己实例化依赖，你（injector）创建它们，然后在合适的时候注入给我吧
    + 构造函数中注入
    + setter 方式注入
    + 接口注入

[轻松学，听说你还没有搞懂 Dagger2](https://blog.csdn.net/briblue/article/details/75578459)

+ @Inject
  + @Inject 给一个类的相应的属性做标记时，说明了它是一个依赖需求方，需要一些依赖
  + @Inject 给一个类的构造方法进行注解时，表明了它能提供依赖的能力
  + @Inject 给一个类的普通方法进行注解时
    + 该方法会在对象注入完成之后调用，可以根据这一特性因此做一些初始化的工作

+ @Component
  + 如果一个方法返回了一个类型，那么其实也算是一种依赖的提供
  + 在方法中传入类型参数。目的是针对这个参数对象进行依赖注入
  + 自动实现类的类名：Dagger+接口名称
  + 创建 Component 都是通过它的 Builder 这个类来进行构建的。其实还有另外一种方式。那就是直接调用 Component 实现类的 create() 方法
  + [Component 之间的依赖](https://johnnyshieh.me/posts/dagger-subcomponent/)
    - 组合 dependencies 
      - 被依赖Component 的生命周期 >= 依赖Component的生命周期
    - 继承 SubComponent
      - 没有生命周期的限制？？？

+ @Provides
  + @Provides 注解的依赖必须存在一个用 @Module 注解的类
  + @Provides 修饰的方法一般用 provide 作用方法名前缀
  + 什么时候用 new 创建对象，什么时候可以直接返回传入的参数就很明显了。对于被 @Inject 注解过构造方法或者在一个 Module 中的被 @Provides 注解的方法提供了依赖时，就可以直接返回传入的参数，而第三方的库或者 SDK 自带的类就必须手动创建了
+ @Module
  + @Module 修饰的类一般用 Module 作为后缀

+ @Singleton
+ @Scope
  + @Singleton 所拥有的单例能力是以 Component 为范围的限定的
  + @Singleton 起作用是因为它被 @Scope 注解，所以，如果可能，我们也可以自己定义 Scope
+ @Qualifiers
  + 处理@Module内两个方法返回一样的类型
+ @Name
+ Lazy 延迟加载

[Google官方MVP+Dagger2架构详解【从零开始搭建android框架系列（6）】](https://www.jianshu.com/p/01d3c014b0b1)

+ 2.2 Dagger2的优点
+ 2.7 作用域（Scopes）
  + 一个没有scope的组件component不可以依赖一个有scope的组件component。子组件和父组件的scope不能相同。我们通常的ApplicationComponent都会使用Singleton注解，也就会是说我们如果自定义component必须有自己的scope
  + [what-determines-the-lifecycle-of-a-component-object-graph-in-dagger-2](https://stackoverflow.com/questions/28411352/what-determines-the-lifecycle-of-a-component-object-graph-in-dagger-2)
+ 2.8 组件依赖（Component Dependencies）
  + 两个依赖的组件不能共享作用域，比如两个组件不能共享@Singleton作用域。依赖的组件需要定义自己的作用域
  + 当创建依赖组件的时候，父组件需要显示的暴露对象给子组件
+ 2.9 子组件（Subcomponents）
  + 需要在父组件的接口中声明（在接口中定义的方法对于生成的对象是可访问的）
  + 能够获取父组件的所有元素（不仅仅是在接口中声明的元素）
+ 3 google官方MVP架构回顾
  + Dagger 2.10之前的标准写法

[【Android】我的Dagger2学习历程：从一头雾水到恍然大悟](https://juejin.im/post/58722866128fe1006b33e104)

我们提到@Inject和@Module都可以提供依赖，那如果我们即在构造函数上通过标记@Inject提供依赖，有通过@Module提供依赖Dagger2会如何选择呢？具体规则如下：

+ 步骤1：首先查找@Module标注的类中是否存在提供依赖的方法。
+ 步骤2：若存在提供依赖的方法，查看该方法是否存在参数。
  + a：若存在参数，则按从步骤1开始依次初始化每个参数；
  + b：若不存在，则直接初始化该类实例，完成一次依赖注入。
+ 步骤3：若不存在提供依赖的方法，则查找@Inject标注的构造函数，看构造函数是否存在参数。
  + a：若存在参数，则从步骤1开始依次初始化每一个参数
  + b：若不存在，则直接初始化该类实例，完成一次依赖注入。

[Dagger2 依赖的接力游戏（六）：Bind、BindInstance、Multibinds注解](https://www.jianshu.com/p/f875cc7f7305)

