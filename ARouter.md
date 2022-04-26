## ARouter

[开源最佳实践：Android平台页面路由框架ARouter](https://yq.aliyun.com/articles/71687)

+ 页面跳转
  
  + 在无法耦合到当前类的时候可以直接使用ARouter的API并通过Path的方式跳转进来。在可以依赖到这个类的场景下，可以直接调用这个类的静态方法跳转到这个页面，这样就解决了我们在日常开发中同一个模块之间的跳转还需要使用Route的非常尴尬的情况，而且这样也可以最终实现所有的页面都被Route管理

+ 从外部导航到内部页面

+ 处理登录逻辑 : 拦截器的运用

+ 标识目标页面信息 : 配置extra参数
  
  + 一个int值就可以提供31个开关。目前而言没有一个目标页面需要配置30多个属性，所以使用int是足够的，而开发者只需要实现一个简单的位运算的工具类就可以提取出二进制int中的每一位，并对其中每一个值进行判断

+ 模块间通信解耦 ：控制反转
  
  + 服务是全局单例的，只有在第一次使用到的时候才会被初始化
  + 拦截器的初始化是在整个SDK启动的时候进行的

+ 解决运行期动态修改路由的问题
  
  + PathReplaceService就是ARouter提供的一个服务，是在ARouter的Frossard层提供的服务，其实就是一个接口，只需要将其实现并标注上就可以，因为有自动注册的机制，所以在APP启动的时候就会注册到ARouter框架上，这样之后框架在跳转的时候就会跳转到这个服务，而如果没有实现，框架就无法调用

+ 解决降级问题

[ARouter/README](https://github.com/alibaba/ARouter/blob/master/README_CN.md)

+ 解析参数
  
  + URL中不能传递Parcelable类型数据，通过ARouter api可以传递Parcelable对象
  + 使用 withObject 传递 List 和 Map 的实现了Serializable 接口的实现类(ArrayList/HashMap)的时候，接收该对象的地方不能标注具体的实现类类型应仅标注为 List 或 Map，否则会影响序列化中类型的判断, 其他类似情况需要同样处理
  + 如果需要传递自定义对象，新建一个类（并非自定义对象类），然后实现 SerializationService,并使用@Route注解标注(方便用户自行选择序列化方式)
  + 需要注意的是，如果不使用自动注入，那么可以不写 ARouter.getInstance().inject(this)，但是需要取值的字段仍然需要标上 @Autowired 注解，因为 只有标上注解之后，ARouter才能知道以哪一种数据类型提取URL中的参数并放入Intent中，这样您才能在intent中获取到对应的参数

+ 预处理服务
  
  + 实现 PretreatmentService 接口，并加上一个Path内容任意的注解即可

+ 推荐在app中实现DegradeService、PathReplaceService

+ 使用绿色通道(跳过所有的拦截器)
  
  ```java
  ARouter.getInstance().build("/home/main").greenChannel().navigation()
  ```

+ 路由中的分组概念
  
  + 一旦主动指定分组之后，应用内路由需要使用 ARouter.getInstance().build(path, group) 进行跳转，手动指定分组，否则无法找到
  + 正确的注解形式应该是 (@Route(path="/test/test"), 如没有特殊需求，请勿指定group字段，废弃功能