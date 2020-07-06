##### 删除已安装 `docker`

---

```
$ sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
```



##### 安装所需的软件包

------

`yum-utils` 提供了 `yum-config-manager` ，并且 ` device mapper` 存储驱动程序需要 `device-mapper-persistent-data` 和 `lvm2`

```
$ sudo yum install -y yum-utils \
  device-mapper-persistent-data \
  lvm2
```



##### 设置稳定的仓库 -- 设置yum源

---

```
$ sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
```



##### 更新`yum` 源

---

```
yum makecache fast
```



##### 安装 Docker Engine-Community

---



```
$ sudo yum install docker-ce docker-ce-cli containerd.io
```



##### 查找 `docker` 特定版本

---

```
$ yum list docker-ce --showduplicates | sort -r
```

```
docker-ce.x86_64            3:19.03.5-3.el7                    docker-ce-stable 
docker-ce.x86_64            3:19.03.5-3.el7                    @docker-ce-stable
docker-ce.x86_64            3:19.03.4-3.el7                    docker-ce-stable 
docker-ce.x86_64            3:19.03.3-3.el7                    docker-ce-stable 
docker-ce.x86_64            3:19.03.2-3.el7                    docker-ce-stable 
docker-ce.x86_64            3:19.03.1-3.el7                    docker-ce-stable 
```



##### 安装 `docker` 特定版本

---

```
$ sudo yum install docker-ce-<VERSION_STRING> docker-ce-cli-<VERSION_STRING> containerd.io
```



##### 启动 `docker` 

---

```
$ sudo systemctl start docker
```



##### 查看 `docker` 版本

---

```
$ docker version
```



##### 增加阿里云镜像

---

 [镜像地址](https://cr.console.aliyun.com/cn-hangzhou/instances/repositories)

##### 通过修改 `daemon` 配置文件 `/etc/docker/daemon.json` 来使用加速器

```json
{ 
	"registry-mirrors": ["https://oh42sv00.mirror.aliyuncs.com"]
}
```



##### 重载文件

---

```
$ systemctl daemon-reload
```



##### 重启 `docker` 

---

```
$ systemctl restart docker
```



##### 创建`docker`组

---

```
$ sudo usermod -aG docker $USER
```



##### 户添加到该`docker`组

---

```
$ usermod -aG docker $USER
```



