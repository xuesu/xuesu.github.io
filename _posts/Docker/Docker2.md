# Docker组件
1. docker client:CLI
2. docker daemon:处理用户请求
3. docker index:中央registry,备份镜像

# Docker要素
1. docker container
2. docker image
3. docker file

# docker命令２
## docker info
## docker logs $sample_job
可以查看命令当前状态
## docker stop $sample_job
## docker restart $sample_job
## docker rm $sample_job
## docker search (image_name)
## docker history (image_name)
## docker commit $sample_job (image_name)
将容器保存为镜像
## docker push (image_name)

# DockerFile
DockerFile+docker build

## 基本格式
    INSTRUCTION argument

1. FROM <image>:<tag>
    - 告诉Docker使用哪个镜像作为基础,第一条必须为FROM指令，可以使用多个FROM指令(每个镜像一次)
2. MAINTAINER <author name>  作者信息
3. RUN <Command>或 RUN ["executable","param1","param2"]  
    - 前者在shell终端运行命令，即 /bin/sh -c；
    - 后者使用exec执行，如 RUN ["/bin/bash", "-c", "echo hello"]
4. CMD   
    - 描述容器启动后运行的服务命令,有三种格式
    ```
    CMD ["executable", "param1", "param2"] 使用exec执行（推荐使用）
    CMD ["/bin/bash","-c","echo hello"]
    CMD command param1 param2  在/bin/sh 中执行，以“/bin/sh -c”方法执行。提供给需要交互的应用
    CMD echo "hello world" 
    CMD ["param1", "param2"]  提供给ENTRYPOINT 的默认参数
    CMD ["-D","--help"]
    ```
    - 指定启动容器时执行的命令，每个Dockerfile 只能有一条 CMD 命令。如果多个则只会执行最后一条
    - 若果用户启动容器时候指定了运行的命令，则会覆盖掉 CMD 指定的命令
5. EXPOSE  向外部开放端口
    - EXPOSE <port> [<port>...]
    - EXPOSE 22 80 8443
6. ENV  指定一个环境变量，会被后续RUN指令使用，并在容器运行时保持
    ```
    EVN <key> <value> 
    ENG PG_MAJOR 9.3.4
    RUN .....
    ENV PATH /usr/local/postgres-$PG-MAJOR/bin/:$PATH
   ```
7. ADD  将复制指定的<src> 到容器的 <dest>，其中<src>可以是Dockerfile所在目录的一个相对路径(文件或目录),也可以是一个URL，还可以是一个tar文件(会自动解压为目录)
    - ADD <src> <dest>
8. COPY  复制本地的主机的 <src> 为容器中的 <dest>。若目标路径不存在时，会自动创建
    - COPY <src> <dest>
9. ENTRYPOINT  容器启动后执行的命令，并且不可被 docker run 提供的参数覆盖。
    - 每个Dockerfile中只能有一个 ENTRYPOINT，当指定多个 ENTRYPOINT时，只有最后一个生效
    ```      
    ENTRYPOINT ["executable", "param1", "param2"]
    ENTRYPOINT command param1 param2  （shell中执行）
    一般是配合CMD使用，CMD提供默认参数，如:
    ENTRYPOINT ["/usr/sbin/sshd"]
    CMD ["-D"]
    ```
10. VOLUME  创建一个可以从本地主机或其他容器挂载的挂载点，一般用来存放数据库和需要保持的数据等
    - VOLUME ["/data"]
11. USER  指定容器运行时的用户名或UID，后续的 RUN也会使用指定用户。使用gosu代替sudo获取管理员权限
    - USER daemon 
12. WORKDIR  指定配置工作目录
    ```
    WORKDIR /path/to/workdir
    WORKDIR /a
    WORKDIR b
    ```
13. ONBUILD  配置当所创建的镜像作为其他新创建镜像的基础镜像时，所执行的操作指令
    ```
    ONBUILD [INSTRUCTION]
    ONBUILD ADD . /app/src
    ONBUILD RUN /usr/local/bin/python-build --dir /app/src
    ```