##### @springBootApplication annotation 组成

- `@EnableAutoConfiguration`: 开启自动配置

- `@ComponentScan`: 在应用程序所在的包上启用`@Component`扫描

- `@Configuration`: 允许在上下文中注册额外的bean或导入额外的配置类

    ```java
    package com.example.myapplication;
    
    import org.springframework.boot.SpringApplication;
    import org.springframework.boot.autoconfigure.SpringBootApplication;
    
    @SpringBootApplication // same as @Configuration @EnableAutoConfiguration @ComponentScan
    public class Application {
    
        public static void main(String[] args) {
            SpringApplication.run(Application.class, args);
        }
    
    }
    ```

    

https://docs.spring.io/spring-boot/docs/2.1.3.RELEASE/reference/htmlsingle/#boot-features-external-config-yaml