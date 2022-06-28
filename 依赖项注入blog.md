# 依赖项注入blog

https://medium.com/@harivigneshjayapalan/dagger-2-for-android-beginners-introduction-be6580cb3edb

文章不错

The best practice here is, when you’re injecting dependencies into clients who have different lifecycle from where dependencies are coming, it’s better to create a separate module and component for them

https://medium.com/tompee/dagger-2-scopes-and-subcomponents-d54d58511781

文章不错

https://github.com/qingmei2/Sample_dagger2

对应的6篇blog不错，细节和原理都讲清楚了

[Dagger 2 完全解析（三）,Component与SubComponent](https://blog.csdn.net/xiaowu_zhu/article/details/93784400)

在 Dagger 2 中 Component 的组织关系分为两种

+ 依赖关系，一个 Component 依赖其他 Compoent公开的依赖实例，用 Component 中的dependencies声明
  + 被依赖的 Component 需要把暴露的依赖实例用显式的接口声明
  + 依赖关系中的 Component 的 Scope 不能相同，因为它们的生命周期不同
+ 继承关系，一个 Component 继承（也可以叫扩展）某 Component 提供更多的依赖，SubComponent 就是继承关系的体现
  + 继承关系中不用显式地提供依赖实例的接口，SubComponent 继承 parent Component 的所有依赖

[Android Dagger2 从零单排(四) Dependencies与SubComponent](https://www.jianshu.com/p/b989e2cb88f6)

@Subcomponent可以使用父@Component所有依赖，父@Component只有@Subcomponent.Builder实例，而不能使用@Subcomponent的依赖
