# 轻松学Dagger2

https://blog.csdn.net/briblue/article/details/75578459



+ @Inject
  + @Inject 给一个类的相应的属性做标记时，说明了它是一个依赖需求方，需要一些依赖
  + @Inject 给一个类的构造方法进行注解时，表明了它能提供依赖的能力
  + @Inject 给一个类的普通方法进行注解时
    + 该方法会在对象注入完成之后调用，可以根据这一特性因此做一些初始化的工作
+ @Component
  + 如果一个方法返回了一个类型，那么其实也算是一种依赖的提供
  + 在方法中传入类型参数。目的是针对这个参数对象进行依赖注入
  + 自动实现类的类名：Dagger+接口名称
+ @Provides
  + Dagger2 依赖查找的顺序是先查找 Module 内所有的 @Provides 提供的依赖，如果查找不到再去查找 @Inject 提供的依赖
  + @Provides 注解的依赖必须存在一个用 @Module 注解的类
  + 什么时候用 new 创建对象，什么时候可以直接返回传入的参数就很明显了。对于被 @Inject 注解过构造方法或者在一个 Module 中的被 @Provides 注解的方法提供了依赖时，就可以直接返回传入的参数，而第三方的库或者 SDK 自带的类就必须手动创建了
+ @Module
+ @Singleton
+ @Scope
  + @Singleton 所拥有的单例能力是以 Component 为范围的限定的
  + @Singleton 起作用是因为它被 @Scope 注解，所以，如果可能，我们也可以自己定义 Scope
+ @Qualifiers
  + 处理@Module内两个方法返回一样的类型
+ @Name
+ Lazy 延迟加载