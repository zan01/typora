```java
public interface WebApplicationInitializer {

	/**
	 * Configure the given {@link ServletContext} with any servlets, filters, listeners
	 * context-params and attributes necessary for initializing this web application. See
	 * examples {@linkplain WebApplicationInitializer above}.
	 * @param servletContext the {@code ServletContext} to initialize
	 * @throws ServletException if any call against the given {@code ServletContext}
	 * throws a {@code ServletException}
	 */
	void onStartup(ServletContext servletContext) throws ServletException;

}
```

WebApplicationInitializer 接口位于`spring-web` 包下

同一包中有 `SpringServletContainerInitializer` 继承 `ServletContainerInitializer` 

`@HandlesTypes(WebApplicationInitializer.class)` SpringServletContainerInitializer只关心类路径下WebApplicationInitializer接口相关的实现类。因此Web容器在回调SpringServletContainerInitializer.onStartup方法时会将类路径下匹配的WebApplicationInitializer接口相关实现类传入onStartup方法中

```java
@HandlesTypes(WebApplicationInitializer.class)
public class SpringServletContainerInitializer implements ServletContainerInitializer {
	@Override
	public void onStartup(@Nullable Set<Class<?>> webAppInitializerClasses, ServletContext servletContext)
			throws ServletException {

		List<WebApplicationInitializer> initializers = new LinkedList<>();

		if (webAppInitializerClasses != null) {
			for (Class<?> waiClass : webAppInitializerClasses) {
				// Be defensive: Some servlet containers provide us with invalid classes,
				// no matter what @HandlesTypes says...
                //过滤接口
				if (!waiClass.isInterface() && 
                    //过滤抽象类
                    !Modifier.isAbstract(waiClass.getModifiers()) &&
                    	//过滤非WebApplicationInitializer实现
						WebApplicationInitializer.class.isAssignableFrom(waiClass)) {
					try {
                        //通过反射进行实例化并放置到list中
						initializers.add((WebApplicationInitializer)										         ReflectionUtils.accessibleConstructor(waiClass).newInstance());
					}
					catch (Throwable ex) {
						throw new ServletException("Failed to instantiate WebApplicationInitializer class", ex);
					}
				}
			}
		}

		if (initializers.isEmpty()) {
			servletContext.log("No Spring WebApplicationInitializer types detected on classpath");
			return;
		}

		servletContext.log(initializers.size() + " Spring WebApplicationInitializers detected on classpath");
        //排序
		AnnotationAwareOrderComparator.sort(initializers);
        //循环启动onStartup方法
		for (WebApplicationInitializer initializer : initializers) {
			initializer.onStartup(servletContext);
		}
	}

}

```

##### WebApplicationInitializer实现类

```java
public class MyWebApplicationInitializer implements WebApplicationInitializer {

    @Override
    public void onStartup(ServletContext servletCxt) {

        // Load Spring web application configuration
        AnnotationConfigWebApplicationContext ac = new AnnotationConfigWebApplicationContext();
        ac.register(AppConfig.class);
        ac.refresh();

        // Create and register the DispatcherServlet
        DispatcherServlet servlet = new DispatcherServlet(ac);
        ServletRegistration.Dynamic registration = servletCxt.addServlet("app", servlet);
        registration.setLoadOnStartup(1);
        registration.addMapping("/app/*");
    }
}
```





