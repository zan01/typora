##### InitializingBean接口

---

> 进一步调整实例状态

afterPropertiesSet()` 执行的时机为实现 `InitializingBean` 接口的当前类实例化的时候

```java
public interface InitializingBean {
    void afterPropertiesSet() throws Exception;
}
```

###### 结合策略模式在spring中使用

---

> 策略模式UML

![image-20200622205023308](/Users/naixuanzan/Documents/typora/spring/image-20200622205023308.png)







