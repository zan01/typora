*Maven**

---

1. 什么是Maven?

    > Maven是基于项目对象模型(POM)，可以通过一小段描述信息来管理项目的构建、报告和文档的软件项目管理工具

    ```
    1.Apache组织中的一个颇为成功的开源项目
    
    2.Maven主要服务于基于Java平台的项目构建、依赖管理和项目信息管理。
    ```

2. Maven 作用?

    ```
    1.提供了一套标准化的项目结构；
    2.提供了一套标准化的构建流程（编译，测试，打包，发布……）；
    3.提供了一套依赖管理机制
    ```

     2.1. 项目构建

    ```
    1.文档和代码的生成
    2.代码的编译、测试和打包
    3.打包好的代码进行分发或者部署
    ```

    2.2. 依赖管理

    > 自动帮我们做依赖管理，我们需要做的就是在pom文件里指定依赖jar包的名称、版本号，Maven会自动寻址下载

    >  Maven 中依赖关系:

    | 作用范围      | 说明                                          |
    | ------------- | --------------------------------------------- |
    | compile(默认) | 编译需要用到的jar                             |
    | test          | 编译Test时需要的jar                           |
    | runtime       | 编译不需要,在运行时需要该jar                  |
    | provided      | 编译时需要用到，但运行时由JDK或某个服务器提供 |

    > 栗子:

    test

    ```xml
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter-api</artifactId>
        <version>5.3.2</version>
        <scope>test</scope>
    </dependency>
    ```

    runtime

    ```xml
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>5.1.48</version>
        <scope>runtime</scope>
    </dependency>
    ```

    provided

    ```xml
    <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>javax.servlet-api</artifactId>
        <version>4.0.0</version>
        <scope>provided</scope>
    </dependency>
    ```

3. Maven 项目基本结构

    ```java
    maven-project(项目名称)
    ├── pom.xml(项目描述文件)
    ├── src
    │   ├── main
    │   │   ├── java(java源码存放位置)
    │   │   └── resources(资源文件存放位置)
    │   └── test
    │       ├── java(java测试源码存放位置)
    │       └── resources(测试资源文件存放位置)
    └── target(编译,打包好的文件存放位置)
    ```

    > 项目描述文件 pom.xml 描述
    >
    > https://maven.apache.org/settings.html

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
             xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
        <modelVersion>4.0.0</modelVersion>
        <parent>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-parent</artifactId>
            <version>2.3.1.RELEASE</version>
        </parent>
        <groupId>com.wpg</groupId>
        <artifactId>demo</artifactId>
        <version>0.0.1-SNAPSHOT</version>
        <name>wpgDemo</name>
        <description>Demo project for WPG</description>
    
        <properties>
            <java.version>1.8</java.version>
        </properties>
    
        <dependencies>
            <dependency>
                <groupId></groupId>
                <artifactId></artifactId>
                <scope></scope>
                <exclusions>
                    <exclusion>
                        <groupId></groupId>
                        <artifactId></artifactId>
                    </exclusion>
                </exclusions>
            </dependency>
        </dependencies>
    
        <build>
            <plugins>
                <plugin>
                    <groupId></groupId>
                    <artifactId></artifactId>
                </plugin>
            </plugins>
        </build>
    </project>
    
    ```

4. Maven 唯一坐标标识

    > 通过groupId,artifactId,version 3个元素确定具体jar包
    >
    > version:-SNAPSHOT 表明为快照版本,每次构建都会重复下载

    ```xml
    <dependency>
        <groupId>com.wpg</groupId><!--Java的包名，通常是公司或组织名称-->
        <artifactId>demo</artifactId><!--Java的类名，通常是项目名称或模块名称-->
        <version>1.0</version><!-- 具体项目或模块的版本差异-->
    </dependency>
    ```

5. Maven Setting 配置

    > 路径: apache-maven/conf/settings.xml

    setting 配置文件基本结构

    ```xml
        <settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0
                              https://maven.apache.org/xsd/settings-1.0.0.xsd">
          <localRepository/>
          <interactiveMode/>
          <offline/>
          <pluginGroups/>
          <servers/>
          <mirrors/>
          <proxies/>
          <profiles/>
          <activeProfiles/>
        </settings>
    ```

    > Level 级别

    1. The Maven install

        ```
        1.${maven.home}/conf/settings.xml
        ```

    2. A user’s install(default)

        ```
        ${user.home}/.m2/settings.xml
        ```

    > 配置项

     1. **localRepository**

         定义存放在本地的jar仓库地址

        ```xml
        <localRepository>${user.home}/.m2/repository</localRepository>
        ```

    2. **interactiveMode**

        是否开启用户交互输入

        ```xml
        <interactiveMode>true</interactiveMode>
        ```

    3. **offline**

          是否脱机运行(是否支持联网进行 artifact 下载、 部署等操作, 默认: false)

        ```xml
        <offline>false</offline>
        ```

    4. **Plugin Groups**

        包含一个pluginGroup元素列表，每个元素都包含一个groupId。当使用插件且命令行中未提供groupId时，将搜索该列表。此列表自动包含org.apache.maven.plugins和org.codehaus.mojo。

        ```xml
        <pluginGroups>
            <pluginGroup>org.eclipse.jetty</pluginGroup>
        </pluginGroups>
        ```

    5. **Services**

        连接服务器配置

        ```xml
          <servers>
            <server>
              <!--服务器id,该id与Maven尝试连接的存储库/镜像的id相匹配-->
              <id>server001</id>
              <!--用户名，密码：这些元素成对出现，表示验证该服务器所需的登录名和密码-->
              <username>my_login</username>
              <password>my_password</password>
              <!-- 密匙配置项-->
              <privateKey>${user.home}/.ssh/id_dsa</privateKey>
              <passphrase>some_passphrase</passphrase>
              <!-- 创建仓库文件和目录时会使用到的权限 -->
              <!-- 配置文件权限 -->
              <filePermissions>664</filePermissions>
              <!-- 配置路径权限 -->
              <directoryPermissions>775</directoryPermissions>
              <configuration></configuration>
            </server>
          </servers>
        ```

    6. Mirrors

        > 从远程仓库才下载 artifacts 时, 用于替代指定远程仓库的镜像服务器配置；
        >
        > 优先级:repository（setting.xml） < repository（pom.xml） < mirror（setting.xml）
        >
        > mirrorOf = *,拦截所以仓库地址请求到配置的当前镜像

        ```xml
        <!-- 
        | 【mirro 匹配顺序】: 
        | 多个 mirror 优先级 按照 id字母顺序进行排列（即与编写的顺序无关）
        | 在第一个 mirror 找不到 artifact, 不会继续超找下一个镜像。
        | 只有当 mirror 无法链接的时候, 才会尝试链接下一个镜像, 类似容灾备份。
        |-->
        <mirrors>
            <mirror>
                <!-- 镜像唯一id-->
                <id>planetmirror.com</id>
                <!-- 镜像名称-->
                <name>PlanetMirror Australia</name>
                <!-- 被镜像服务器地址 -->
                <url>http://downloads.planetmirror.com/pub/maven2</url>
                <!-- 比较重要
        		| *           = 匹配所有远程仓库。 这样所有 pom 中定义的仓库都不生效
                | external:*  = 匹配除 localhost、使用 file:// 协议外的所有远程仓库
                | repo1,repo2 = 匹配仓库 repo1 和 repo2
                | *,!repo1    = 匹配所有远程仓库, repo1 除外
                |-->
                <mirrorOf>central</mirrorOf>
            </mirror>
        </mirrors>
        ```

        栗子:

        aliyun镜像

        ```xml
        <mirror>
            <id>aliyun</id>
            <mirrorOf>central</mirrorOf>
            <name>aliyun public</name>
            <url>http://maven.aliyun.com/nexus/content/groups/public</url>
        </mirror>
        ```

    7. **Proxies**

        > 用来配置不同的代理, 多代理 profiles 可以应对笔记本或移动设备的工作环境: 通过简单的设置 profile id 就可以很容易的更换整个代理配置

        ```xml
          <proxies>
            <proxy>
              <!-- 唯一id -->
              <id>myproxy</id>
              <!-- 是否激活 -->
              <active>true</active>
              <!-- 代理协议 -->
              <protocol>http</protocol>
              <!-- 代理地址 -->
              <host>proxy.somewhere.com</host>
              <!-- 代理端口 -->
              <port>8080</port>
              <!-- 认证登录名和密码 -->
              <username>proxyuser</username>
              <password>somepassword</password>
              <!-- 不被代理的地址列表 | 隔开 -->
              <nonProxyHosts>*.google.com|ibiblio.org</nonProxyHosts>
            </proxy>
          </proxies>
        ```

    8. **Profiles**

        ```xml
        <!--
             | 构建方法的配置清单, maven 将根据不同环境参数来使用这些构建配置。
             | settings.xml 中的 profile 元素是 pom.xml 中 profile 元素的裁剪版本。
             | settings.xml 负责的是整体的构建过程, pom.xml 负责单独的项目对象构建过程。
             | settings.xml 只包含了id, activation, repositories, pluginRepositories 和 properties 元素。
             | 
             | 如果 settings 中的 profile 被激活, 它的值会覆盖任何其它定义在 pom.xml 中或 profile.xml 中的相同 id 的 profile。
             |
             | 查看当前激活的 profile:
             |   mvn help:active-profiles
             |-->
        <profiles>
            <profile>
                <!-- 唯一 id -->
                <id>test</id>
                <!--
                | profile 的激活条件配置；
                | 其他激活方式: 
                | 1. 通过 settings.xml 文件中的 activeProfile 元素进行指定激活。
                | 2. 在命令行, 使用-P标记和逗号分隔的列表来显式的激活, 如: mvn clean package -P 					myProfile）。 
                |-->
                <activation>
                    <!-- 是否默认激活 -->
                    <activeByDefault>false</activeByDefault>
                    <!-- 内建的 java 版本检测 -->
                    <jdk>1.8</jdk>
                    <os>
                        <!-- 操作系统 -->
                        <name>Windows XP</name>
                        <!-- 操作系统家族 -->
                        <family>Windows</family>
                        <!-- 操作系统 -->
                        <arch>x86</arch>
                        <!-- 操作系统版本 -->
                        <version>5.1.2600</version>
                    </os>
                    <property>
                        <name>mavenVersion</name>
                        <value>2.0.3</value>
                    </property>
                    <file>
                        <!-- 根据文件存在/不存在激活profile -->
                        <exists>${basedir}/file2.properties</exists>
                        <!-- 如果指定的文件不存在, 则激活profile -->
                        <missing>${basedir}/file1.properties</missing>
                    </file>
                </activation>
                ...
            </profile>
        </profiles>
        ```

    9. **Properties**

        ```xml
        <profiles>
          	<!-- 在当前 profile 被激活时,  ${profile.property} 就可以被访问到了 -->
            <profile>
                <properties>
                    <user.install>${user.home}/our-project</user.install>
                </properties>
                ...
            </profile>
        </profiles>
        ```

    10. **Repositories** 

        > 远程仓库列表

        ```xml
        <!--
        | releases vs snapshots
        | maven 针对 releases、snapshots 有不同的处理策略, POM 就可以在每个单独的仓库中, 为每种类型的       		artifact 采取不同的策略
        | 例如: 
        |     开发环境 使用 snapshots 模式实时获取最新的快照版本进行构建
        |     生成环境 使用 releases 模式获取稳定版本进行构建
        |-->
        <profiles>
            <profile>
              ...
              <repositories>
                <repository>
                  <!-- 远程仓库唯一标识 -->
                  <id>codehausSnapshots</id>
                  <!-- 远程仓库名称 -->
                  <name>Codehaus Snapshots</name>
                  <!-- 如何处理远程仓库里发布版本的下载 -->
                  <releases>
                    <!-- 是否允许该仓库为 artifact 提供 发布版下载功能 -->
                    <enabled>false</enabled>
                    <!-- 
                   | 每次执行构建命令时, Maven 会比较本地 POM 和远程 POM 的时间戳, 该元素指定比较的频					率。
                   | 有效选项是: 
                   |     always（每次构建都检查）, daily（默认, 距上次构建检查时间超过一天）, 						interval: x（距上次构建检查超过 x 分钟）、 never（从不）
                   |
                   | 重要: 
                   |     设置为 daily, 如果 artifact 一天更新了几次, 在一天之内进行构建, 也不会从仓库					中重新获取最新版本
                   |-->
                    <updatePolicy>always</updatePolicy>
                    <!-- 当 Maven 验证 artifact 校验文件失败时该怎么做: ignore（忽略）, fail（失				败）, 或者warn（警告） -->
                    <checksumPolicy>warn</checksumPolicy>
                  </releases>
                  <snapshots>
                    <enabled>true</enabled>
                    <updatePolicy>never</updatePolicy>
                    <checksumPolicy>fail</checksumPolicy>
                  </snapshots>
                  <!-- 远程仓库URL -->
                  <url>http://snapshots.maven.codehaus.org/maven2</url>
                  <!-- 
                  | 用于定位和排序 artifact 的仓库布局类型-可以是 default（默认）或者 legacy（传统）
                  | Maven 2为其仓库提供了一个默认的布局；然而, Maven 1.x有一种不同的布局。我们可以使用该				元素指定布局是default（默认）还是legacy（传统）
                  | -->
                  <layout>default</layout>
                </repository>
              </repositories>
              <pluginRepositories>
                ...
              </pluginRepositories>
              ...
            </profile>
          </profiles>
        ```

    11. **Active Profiles**

        ```xml
        <!--
        | 手动激活 profiles 的列表, 按照 profile 被应用的顺序定义 activeProfile
        | 任何 activeProfile, 不论环境设置如何, 其对应的 profile 都会被激活, maven 会忽略无效（找不到）的 profile
        |--> 
        <activeProfiles>
            <activeProfile>env-test</activeProfile>
          </activeProfiles>
        ```

6. *Maven 构建生命周期**

    1. 三套生命周期

        > clean生命周期

        | 命令       | 描述                         |
        | ---------- | ---------------------------- |
        | pre-clean  | 执行一些清理前需要完成的工作 |
        | clean      | 清理上一次构建生成的文件     |
        | post-clean | 执行一些清理后需要完成的工作 |

        > default 生命周期

        | 命令                  | 描述               |
        | --------------------- | ------------------ |
        | validate              |                    |
        | initialize            |                    |
        | generate-sources      |                    |
        | process-sources       | 处理项目主资源文件 |
        | generate-resources    |                    |
        | process-resources     |                    |
        | compile               | 编译项目的主源码   |
        | process-classes       |                    |
        | generate-test-sources |                    |
        | .........             |                    |

        > site生命周期

        | 命令        | 描述                                     |
        | ----------- | ---------------------------------------- |
        | pre-site    | 执行一些在生成项目站点之前需要完成的工作 |
        | site        | 生成项目站点文档                         |
        | post-site   | 执行一些在生成项目站点之后需要完成的工作 |
        | site-deploy | 执行一些在生成项目站点之后需要完成的T    |

        | 生命周期阶**E** | 殳 插件目标              | 生命周期阶段 | 插件目标                 |
        | --------------- | ------------------------ | ------------ | ------------------------ |
        | pre-clean       |                          | pre-site     |                          |
        |                 |                          | site         | maven-site-plugin: site  |
        | clean           | maven-clean-plugin:clean | post-site    |                          |
        |                 |                          |              |                          |
        | post-clean      |                          | sile-deploy  | maven-site-plugin:deploy |

        2. default生命周期的内置插件绑定关系

            | 生命周期阶段          | 插件日标                              | 执行任务                       |
            | --------------------- | ------------------------------------- | ------------------------------ |
            | proeess-resources     | maven-rrsources-plugin:resources      | 复制主资源文件至主输出日录     |
            | compile               | maven-compiler-plugin :compile        | 编译主代码至主输出日录         |
            | proess-test-resources | maven-resources-plugin: testResourres | 复制测试资源文件至测试输出目录 |
            | test-compile          | maven-compiler: testCompile           | 编译测试代码至测试输出目录     |
            | test                  | maven-surefire-plugin:test            | 执行测试用例                   |
            | package               | maven-jar-plugin:jar                  | 创建项目jar包                  |
            | install               | maven-insiall-plugin: install         | 将项目输出构件安装到本地仓库   |
            | deploy                | mavcn-dfploy-plugin:deploy            | 将项目输出构件部署到远程仓库   |

7. **Maven 聚合**

    ```
    mutiple-project
    ├── module-a
    │   ├── pom.xml
    │   └── src
    ├── module-b
    │   ├── pom.xml
    │   └── src
    └── module-c
        ├── pom.xml
        └── src
    ```

8. Parent pom.xml

    ```xml
    <project xmlns="http://maven.apache.org/POM/4.0.0"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
        <modelVersion>4.0.0</modelVersion>
    
        <groupId>com.wpg</groupId>
        <artifactId>demo</artifactId>
        <version>1.0</version>
        <packaging>pom</packaging>
    
        <name>parent</name>
    
        <properties>
            <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
            <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
            <maven.compiler.source>11</maven.compiler.source>
            <maven.compiler.target>11</maven.compiler.target>
            <java.version>11</java.version>
        </properties>
        <modules>
            <!-- 路径为相对路径 -->
        	<module>../A</module>
        	<module>../B</module>
        	<module>../C</module>
    	</modules>
    </project>
    ```

2. model A

    ```xml
    <project xmlns="http://maven.apache.org/POM/4.0.0"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
        <modelVersion>4.0.0</modelVersion>
        <parent>
            <groupId>com.wpg</groupId>
            <artifactId>demo</artifactId>
            <version>1.0</version>
            <relativePath>../parent/pom.xml</relativePath>
        </parent>
        <artifactId>module-a</artifactId>
        <packaging>jar</packaging>
        <name>module-a</name>
    </project>
    ```

8. **Maven 继承**

    1. Parent pom.xml	

        ```xml
        <project xmlns="http://maven.apache.org/POM/4.0.0"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
            <modelVersion>4.0.0</modelVersion>
        
            <groupId>com.wpg</groupId>
            <artifactId>demo</artifactId>
            <version>1.0</version>
            <packaging>pom</packaging>
        
            <name>parent</name>
        
           	<dependencyManagement>
            <dependencies>
                <dependency>
                    <groupId>junit</groupId>
                    <artifactId>junit</artifactId>
                    <version>3.8.1</version>
                </dependency>
            </dependencies>
        </dependencyManagement>
        </project>
        ```

    2. model A

        ```xml
        <project xmlns="http://maven.apache.org/POM/4.0.0"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
            <modelVersion>4.0.0</modelVersion>
            <parent>
                <groupId>com.wpg</groupId>
                <artifactId>parent</artifactId>
                <version>1.0</version>
                <relativePath>../parent/pom.xml</relativePath>
            </parent>
            <artifactId>module-a</artifactId>
            <packaging>jar</packaging>
            <name>module-a</name>
        </project>
        ```

9. **Nexus 私服**

     1. 为什么使用Nexus？

        > 节省外网带宽

        大量对于外部仓库的重复请求会消耗带宽，利用私服代理外部仓库，可以消除对外的重复构件下载，降低带宽的压力

        > 加速Maven构建

        不停地连接请求外部仓库十分的耗时，Maven在执行构建的时候不停地检查远程仓库的数据。利用私服，Maven只检查局域网的数据，提高构建的速度。

        > 部署第三方构件

        当某个构件无法从任何一个外部远程仓库获得。建立私服之后，便可以将这些构件部署到私服，供内部的Maven项目使用。

        > 提高稳定性，增强控制

        Maven构建高度依赖于远程仓库，因此，当网络不稳定的时候，Maven构建也会变得不稳定，甚至无法构建。私服缓存了大量构建，即使暂时没有网络，Maven也可以正常的运行。

        > 降低中央仓库的负荷

        使用私服可以避免很多对中央仓库的重复下载，降低中央仓库的压力。

    2. **默认内置仓库**

        > Maven Central

        该仓库代理Maven中央仓库，其策略为Release,因此只会下载和缓存中央仓库中的发布版本构件

        > Releases

        这是一个策略为Release的主类型仓库，用来部署组织内部的发布版本构件

        > Snapshots

        这是一个策略为Snapshot的宿主类型仓库.用来部署组织内部的快照版 本构件

        > 3rd party

        这是一个策略为Release的宿主类型仓库，用来部署无法从公共仓库获得 的第三方发布版本构件

        > Apache Snapshots

        这是个策略为Snapshot的代理仓库，用来代理Apache Maven仓 库的快照版本构件

        > Codehaus Snapshots

        这是一个策略为Snapshot的代理仓库，用来代理Codehaus Maven 仓库的快照版本构件

        > Google Code

        这是一个策略为Release的代理仓库，用来代理Google Code Maven仓库的发布版本构件

        > java, net - Maven 2

        这是一个策略为Release的代理仓库,用来代理java, net Maven 仓库的发布版本构件

        > Public Repositories

        该仓库将上述所冇策略为Release的仓库聚合并通过一致的地 址提供服务

        > Public Snapshot Repositories

        该仓库组将上述所有策略为Snapshot的仓库聚合并通过一致的地址提供服务.

    3. **Nexus仓库分类**

        ![image-20200702100902029](/Users/naixuanzan/Documents/typora/maven/image-20200702100902029.png)

10. WPG nexus

    1. 后端开发组使用(maven私有仓库仓库)：

    > https://maven.cloud4water.com/
    >
    > guest账户(只读)
    >
    > 账号:wpg-guest
    >
    > 密码:wpg@guest       

    2. setting.xml 配置

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

    3. setting.xml 账户配置

        ```xml
        <servers>
            <server>
                <id>wpg-maven-public</id>
                <username>wpg-guest</username>
                <password>wpg@guest</password>
            </server>
        </servers>
        ```

        















































