# Spring

### 1.Spring 是如何创建一个Bean对象的

​	1.Spring Bean元信息（BeanDedfinition）读取阶段

​		Spring容器刚启动的时候，Spring会按照我们声明Bean的方式去读取我们的bean声明信息（@Bean 		@Componet。。。），然后封装到BeanDefinition中，在创建Bean对象的时候，会根据			                    	        BeanDefinition进行配置

​	2.Spring Bean注册阶段

​		每一个Bean，spring都会生成对应的BeanDefinition对象，Spring通过一个map来存储每个bean相对应		的BeanDefinition, 该map封装到DefaultListableBeanFactory中，把beanDefinition存储到		  	        beanDefinitionMap中的过程就是注册

​	3.Bean实例化阶段

​		Spring会遍历beanDefinitionMap，通过反射创建Bean实例，并放到SingletonObject的map中

​	3.获取Bean阶段

​		遍历SingletonObject 的map，匹配到目标bean并返回

### 2.什么是单例池，作用是什么

​	单例池就是一个map，存放的是已经实例化的bean，当调用getBean的时候，会根据Key的值找到value，通	过设置key为bean的name来保证bean对象的唯一性（单例）

### 3.Bean对象和普通对象的区别

​	普通的对象需要自行创建和管理，Bean对象是由Spring容器负责创建，配置和管理

​	依赖注入，Spring通过DI来自动解决依赖关系，无需手动注入

​	生命周期管理

### 4.依赖注入是怎么实现的

### 5.@PostConstruct工作原理

### 6.Bean的初始化工作原理

### 7.Bean的初始化和实例化区别

### 8.什么是推断构造方法

### 9.单例Bean和单例模式联系

### 10.ByType ByName

### 11.Spring AOP概念 原理

### 12.Spring事务原理

### 13.同类方法调用为什么事务会失效

### 14.@Configuration注解的作用

### 15.Spring为什么使用三级缓存来解决循环依赖