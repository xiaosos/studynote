## springboot

* 自动装配AutoConfiguration
* starter
* actuator
* 命令行cli



autoConfigurationImportSelector

autoConfigurationpackages.Registrar



importSelector

importBeanDefinitionRegistrar



import 是可以导入其他的一些配置的。

现在需求是：根据上下文来激活不同的bean，带一些条件的东西，进行不同的处理。

spring有2个：ImportSelect，ImportBeanDefinitionRegistrar进行动态注入

在加载configurationbean的时候去做一些事情。



### ConditionOnBean

ConditionMissingBean....



### starter







自动装配：

简单来讲就是将bean放到ioc容器进行托管。

实现自动装配，我做了啥？



1.写一个类实现

ImportSelector，复写其方法，传入注解元数据，返回字符串数组

或者2.写一个实现类，实现autoConfigurationpackages，再RootBeandefinition bean = newRootBeanDefinition（我的要装配的class）；

再注册上去，register（name，bean）；



spi扩展机制：

在META-INF下建立spring.factories里面写上EnableAutoConfiguration=我的对应的Configuration类文件。





```
EnableDefineService上面有import注解，注解里指向cacheimportselect
CacheImportSelect返回规则（返回bean）
CacheService具体bean
```





### Actuator





