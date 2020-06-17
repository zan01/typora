##### 查看运行中的容器

---

```
$ docker ps
```



##### 查看所有容器

---

```
$ docker ps -a
```



##### 终止容器

---

```
$ docker stop 容器名称/容器id
```

![image-20191226210958586](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20191226210958586.png)



##### 启动容器

---

```
$ docker start 容器名称/容器id
```

![image-20191226211159532](C:\Users\EDZ\AppData\Roaming\Typora\typora-user-images\image-20191226211159532.png)



##### 删除容器

---

```
$ docker rm 容器名称/容器id
```

<!--删除容器前 先停止容器 或者 增加 -f 参数进行强制删除-->



##### 进入容器

---

```
$ docker exec -it 容器名称 /bin/bash
```

<!-- 启动容器加参数 -d 启动后会进入后台 -->

<!-- exit 退出容器 -->



##### 创建新的容器

---

```
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
```

<!-- OPTIONS -->

<!-- -d 后台运行容器，并返回容器ID-->

<!-- -i 以交互模式运行容器，通常与 -t 同时使用-->

<!-- -t 为容器重新分配一个伪输入终端，通常与 -i 同时使用-->

<!-- -p 指定端口映射，格式为：主机(宿主)端口:容器端口-->

<!-- --name="名称": 为容器指定一个名称 -->

<!-- -P 随机端口映射，容器内部端口随机映射到主机的高端口 -->

<!-- --volume , -v: 绑定一个卷 -->

<!-- -e 指定环境变量,容器中可以使用该环境变量-->

```
$ docker run -it --rm tomcat:8.0
```

<!-- --rm 运行完成删除容器-->

##### 命令帮助

---

```
$ docker command --help
```

