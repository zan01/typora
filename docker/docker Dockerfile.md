##### Dockerfile 命令组成

---

```java
FROM <image>或 FROM <image>:<tag>
MAINTAINER  <name>
WORKDIR /path/work
RUN <command> 或 RUN [""， ""， ""]
CMD ["","",""]
EXPOSE <port>  [ <port> ...]
ENV <key> <value>
ENTRYPOINT ["","",""]
ADD <src>  <dest>
COPY <src>  <dest>
VOLUME ["/mnt"] 
USER demo
ONBUILD [INSTRUCTION]

```

<!-- FROM 基础镜像 -->

<!-- MAINTAINER 维护者信息 -->

<!-- WORKDIR为后续的 RUN 、 CMD 、 ENTRYPOINT 指令配置工作目录 -->

<!-- RUN 在当前镜像基础上执行，并提交为新的镜像 -->

<!-- CMD 容器启动时执行的命令,多个CMD 执行，最后一个有效执行 -->

<!-- EXPOSE 预定暴露的端口，做端口映射 -->

<!-- ENV 指定环境变量，会被RUN指令使用，并在容器运行时保存 -->

<!-- ENTRYPOINT 容器启动后执行的命令，不能未外部docker run 提供的参数命令覆盖，ENTRYPOINT 未多个时，最后一个ENTRYPOINT 起效 -->

<!-- ADD 复制文件到容器中，支持tar.gz 和url -->

<!-- COPY 复制Dockerfile所在目录的相对路径文件到容器中（已本地Dockerfile为源目录，使用COPY） -->

<!-- VOLUME 将本地或其他容器的目录挂载到容器中 -->

<!-- USER 运行容器时的用户名-->

<!-- 以当前镜像未基本创建新的镜像是所执行的操作命令，当前Dockerfile不执行-->