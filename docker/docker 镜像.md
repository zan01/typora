##### 查找镜像

---

```
$ docker search tomcat
```



##### 获取镜像到本地

---

```
$ docker pull [OPTIONS] NAME[:TAG|@DIGEST]
```



##### 列出本地`image` 文件

---

```
$ docker images
```



##### 删除 `image`

---

```
$ docker image rm 镜像id
$ docker rmi 镜像id
```



##### docker 生成镜像

---

###### commit方式

启动容器

```
$ docker run --name mytomcat -p 80:8080 -d tomcat
```

修改容器内容

```
$ docker exec -it mytomcat /bin/bash
$ cd  webapps/ROOT
$ rm -f index.jsp  
$ echo hello world > index.html
$ exit
```

提交更新镜像

```
$ docker commit -m="描述信息" -a="作者" mytomcat mytomcat:v1
```













