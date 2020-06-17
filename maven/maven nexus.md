```
maven-central：maven中央库，默认从https://repo1.maven.org/maven2/拉取jar
maven-releases：私库发行版jar，初次安装请将Deployment policy设置为Allow redeploy
maven-snapshots：私库快照（调试版本）jar
maven-public：仓库分组，把上面三个仓库组合在一起对外提供服务，在本地maven基础配置settings.xml或项目pom.xml中使用
```

##### 如果 nexus 服务器可以联网的情况下

```
maven-aliyun
创建 国内 代理镜像
设置 type  为 proxy
Proxy 下的 remote storage  填入 镜像地址 http://maven.aliyun.com/nexus/content/groups/public/
```

```
maven-public 中 增加 上面创建的 maven-aliyun 加入到Members 中,调整顺序放在maven-public 上面
```

```
所有的远程仓库请求都定向到nexus中,进行下载
```

```xml
 <mirror>
        <id>Nexus</id>
         <mirrorOf>*</mirrorOf>
            <name>Nexus public</name>
            <!-- 私服地址-->
            <url>http://192.168.19.131:8081/repository/maven-public/</url>
  </mirror>
```

##### 如果 nexus 服务器不可以联网的情况下	

```xml
不在nexus 中创建镜像代理
再maven setting 中 
1.增加镜像镜像代理所有远程请求访问到aliyun的镜像,除了profile  repository 列表中的nexus
<mirror>
        <id>Nexus</id>
         <mirrorOf>*,!nexus</mirrorOf>
            <name>aliyun public</name>
            <!-- aliyun-->
            <url>http://maven.aliyun.com/nexus/content/groups/public</url>
  </mirror>
```

上传本地项目jar到仓库中配置

1. `setting.xml`中设置远程服务器访问需要的授权信息

   ```xml
      <server>
               <id>maven-releases</id>
               <username>admin</username>
               <password>nexus3</password>
           </server>
           <server>
               <id>maven-snapshots</id>
               <username>admin</username>
               <password>nexus3</password>
           </server>
   ```

2. `pom.xml` 中设置推送的远程服务信息和设置

   ```xml
   <distributionManagement>
           <repository>
               <id>maven-releases</id>
               <name>maven-releases</name>
               <url>http://192.168.19.131:8081/repository/maven-releases/</url>
           </repository>
           <snapshotRepository>
               <id>maven-snapshots</id>
               <name>maven-snapshots</name>
               <url>http://192.168.19.131:8081/repository/maven-snapshots/</url>
           </snapshotRepository>
       </distributionManagement>
   ```

