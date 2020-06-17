1. 直接内嵌Tomcat(不需要部署WAR文件)
2. 提供约定的“starter”依赖项简化第三方MAVEN配置来简化构建配置
3. 尽可能自动配置Spring和第三方库
4. 完全不需要代码生成，也不需要XML配置

```java
com
 +- example
     +- myapplication
         +- Application.java
         |
         +- customer
         |   +- Customer.java
         |   +- CustomerController.java
         |   +- CustomerService.java
         |   +- CustomerRepository.java
         |
         +- order
             +- Order.java
             +- OrderController.java
             +- OrderService.java
             +- OrderRepository.java
```

##### 运行项目

```
$ java -jar target/myapplication-0.0.1-SNAPSHOT.jar
```

