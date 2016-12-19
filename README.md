# united-cache
统一缓存框架 </br>
### cache-core 
</br>
定义了一些缓存框架的基础抽象概念以及缓存元注解，缓存事件元注解，各种缓存实现能基于次框架上进行非常方便的适配，使用者只需要关心缓存容器的实现和配置项，不需要关心配置解析和方法拦截等等底层细节</br>
### cache-spring
</br>
提供了与spring相集成的相关功能</br>
如果以XML方式进行配置，可以在配置文件中引入</br>
bean class="org.cacheframework.bootstrap.CacheBootstrap" </br>
如果以注解方式进行配置，可以在配置类上打上注解@EnableCache<br>
具体使用可以看测试用例</br><br>
扩展性

启动器类org.cacheframework.bootstrap.CacheBootstrap下的所有提供的组件都是可以复写实现的，整个架构是松散，高内聚，低耦合的，另外还提供自定义的缓存事件，一个类实例范围内有一条缓存事件总线，可以自定义缓存事件，通过注解的方式发送缓存事件，可以通过向缓存事件总线注册监听来监听缓存事件。<br>
本缓存框架的缓存组件和缓存事件都是可以通过以元注解形式来进行扩展，自带的开箱即用的几个缓存组件(@SoftCache)和缓存事件(@FlushCacheEvent)是通过这种方式扩展而来。详例请看@SoftCache,@FlushCacheEvent。两个注解及其扩展。<br>
### 相比spring-cache的优点：
<br>
1.缓存注解使用元注解(@Cache)扩展而来，并且每个缓存注解对应一个缓存工厂，缓存工厂可通过缓存注解来解析缓存配置，每一个缓存注解的配置项互不相关，配置项非常灵活，完全自定义，用户可以根据自定客制化的缓存来定义缓存注解中的各种配置项<br>
2.缓存事件总线，spring-cache只有刷新缓存这个概念，而在本缓存框架中，刷新只是缓存事件中的一种，可以自己通过元注解(@CacheContextEvent)进行客制化，然后来进行处理。<br>
3.额外的拦截处理，用户可以通过实现接口 ICacheInterceptor 自己定义想要拦截的感兴趣的方面，具体的扩展方式可参考 CacheBootstrap 中的注册方式。<br>
4.本缓存的微核心为 org.cacheframework.bootstrap.aop.DefaultInvoker 它定义了一种对关心点的拦截和调用方式，整个框架都是基于此核心扩展而来，并且整个框架的各组件均在 CacheBootstrap 中暴露给用户，均可以进行复写和重用，扩展性极强，对第三方也非常友好。
### cache-guice
</br>
提供了与guice的相关集成（待开发）</br>
