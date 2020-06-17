#### docker 安装nexus3

##### 从`docker hub` 获取 `nexus`

1. 查找 `nexus3`

    ```
    $ docker search nexus
    ```

    ![image-20200110193914494](C:\Users\EDZ\iCloudDrive\学习文档\docker\image-20200110193914494.png)

2. 获取`nexus3`

    ```
    $ docker pull sonatype/nexus3
    ```

3. 查看下载的镜像

    ```
    $ docker images
    ```

    ![image-20200110193419159](C:\Users\EDZ\iCloudDrive\文档\docker\image-20200110193419159.png)

##### 启动`docker nexus3`

```
$ docker run --privileged=true --name mynexus --restart=always -d -p 8081:8081  -v nexus-data:/nexus-data sonatype/nexus3
```

<!-- nexus-data 创建的docker volume -->

<!-- --restart=always docker 启动时mynexus 也会启动-->

<!-- --privileged=true 特权级运行-->

##### 查看nexus3默认密码

```
密码存放路径为挂载目录中 /var/lib/docker/volume/nexus_data/_data/admin.password
```





