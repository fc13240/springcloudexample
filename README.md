# springcloudexample
spring cloud 学习例子<br>
在微服务架构中，需要几个关键的组件，服务注册与发现、服务消费、负载均衡、断路器、智能路由、配置管理等，<br>
由这几个组件可以组建一个简单的微服务架构。<br>
## 服务发现（Eureka、consul）<br>
+ eureka-server(服务注册中心) http://localhost:1001/ <br>
+ eureka-client(服务提供方)http://localhost:2001/demo <br>
+ eureka-consumer(服务消费者-手动负载均衡)http://localhost:2101/consumer <br>
+ eureka-consumer-ribbon(服务消费者-自动负载均衡)http://localhost:2102/ribbon <br>
+ Eureka简介:http://www.cnblogs.com/wangdaijun/p/6851027.html<br>
+ Eureka简介:http://www.roncoo.com/article/detail/128041<br>
+ **Note:先启动注册中心然后启动服务提供者**<br>

### consul-client(consul服务提供方)
+ Spring Cloud Consul项目是针对Consul的服务治理实现<br>
+ Consul特性:服务发现,健康检查,Key/Value存储,多数据中心<br>
+ 由于Consul自身提供了服务端，所以我们不需要像之前实现Eureka的时候创建服务注册中心，<br>
+ 直接通过下载consul的服务端程序就可以使用:<br>
+ consul怎么在windows下安装:http://blog.csdn.net/forezp/article/details/70188595<br>
+ consul下载地址：https://www.consul.io/downloads.html<br>
+ windows pc 环境变量设置 在path下加上：E:\programfiles\consul； cmd启动运行 consul agent -dev<br>
+ consul默认地址：http://localhost:8500<br>
+ 访问demo:http://localhost:3001/demo<br>
+ 服务发现系统consul介绍:http://www.tuicool.com/articles/j2YVB3<br>

## 声明式REST客户端-Feign的使用<br>
+ Feign是一种声明式、模板化的HTTP客户端。<br>
+ 在Spring Cloud中使用Feign, 我们可以做到使用HTTP请求远程服务时能与调用本地方法一样的编码体验，开发者完全感知不到这是远程方法，更感知不到这是个HTTP请求。<br>
+ eureka-consumer-feign(服务消费者-feign): http://localhost:2103/feign?name=jon<br>
+ **feign是自带断路器的**，此版本hystrix是关闭的 ，如果使用feign想用断路器的话，可以在配置文件中开启它,配置如下：feign.hystrix.enabled=true<br>

## 断路器（Hystrix）<br>
+ eureka-consumer-ribbon-hystrix(服务消费者-断路器)<br>
+ http://localhost:2104/ribbon?name=jon<br>

## 智能路由（zuul）<br>
+ Zuul的主要功能是路由和过滤器。
+ 路由功能是微服务的一部分，比如／api/user映射到user服务，/api/shop映射到shop服务。zuul实现了负载均衡。

+ 依次启动顺序 eureka-server、eureka-client、eureka-consumer、eureka-consumer-feign、eureka-zuul工程
  依次访问下面的路径查看测试效果。
+ http://localhost:3101/baidu
+ http://localhost:3101/index
+ http://localhost:3101/api-a/consumer
+ http://localhost:3101/api-b/feign?name=jon

## 客户端负载均衡（Ribbon）<br>

