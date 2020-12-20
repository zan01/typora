#### 后端开发组使用(maven私有仓库仓库)

---

##### 地址

>   https://maven.cloud4water.com/

##### guest账户账号

> wpg-guest
>
> wpg@guest

##### deploy账户

>wpg-deploy-maven
>
>wpg@7DcXd3gXUr9fOqT

```xml
<mirrors>
    <mirror>
        <id>wpg-maven-public</id>
        <mirrorOf>central</mirrorOf>
        <name>WPG-MAVEN-REPO</name>
        <url>https://maven.cloud4water.com/repository/wpg-maven-public/</url>
    </mirror>
</mirrors>
```

```xml
<servers>
    <server>
        <id>wpg-maven-public</id>
        <username>wpg-guest</username>
        <password>wpg@guest</password>
    </server>
</servers>
```

前端开发组使用

---

##### 地址

> https://npm.cloud4water.com/

##### guest账号

> wpg-guest
>
> wpg@guest

##### deploy地址

> wpg-deploy-npm
>
> wpg@Iku5ph0TjYJ6UJa

使用说明：修改本地node源~/.npmrc配置：
1.执行 npm config set registry https://npm.cloud4water.com/repository/wpg-npm-public/

2.编辑~/.npmrc文件，最终结果如下：
registry=https://npm.cloud4water.com/repository/wpg-npm-public/
always-auth=true
_auth=d3BnLWd1ZXN0OndwZ0BndWVzdA==
（注意：不要修改_auth内容，此内容是wpg-guest用户加密过后的密码）