# @import

`@Import` 可以传入四种类型：

+ 普通类 (regular)
+ 配置类 (Configuration)
+ `ImportSelector` 的实现类
+ `ImportBeanDefinitionRegistrar` 的实现类

```java
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
public @interface Import {

	/**
	 * {@link Configuration @Configuration}, {@link ImportSelector},
	 * {@link ImportBeanDefinitionRegistrar}, or regular component classes to import.
	 */
	Class<?>[] value();

}

```

