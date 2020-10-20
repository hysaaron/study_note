# Docker 学习笔记

## 基本概念
Docker 是一个开源的应用容器引擎，基于 Go 语言并遵从 Apache2.0 协议开源。Docker 可以让开发者打包他们的应用以及依赖包到一个轻量级、可移植的容器中，然后发布到任何流行的 Linux 机器上，也可以实现虚拟化。容器是完全使用沙箱机制，相互之间不会有任何接口（类似 iPhone 的 app）,更重要的是容器性能开销极低。[[1]](https://www.runoob.com/docker/docker-tutorial.html)  
我的理解：Docker 便于交付一整套与外界隔离的应用运行环境，省去了大量环境不一致导致的时间损耗。相比于虚拟机的虚拟化方式，它还更加轻便。
### 镜像 (`Image`)
相当于一个 root 文件系统。体积大，设计为分层存储的架构。[[2]](https://yeasy.gitbook.io/docker_practice/basic_concept/image)
### 容器 (`Container`)
**镜像** (`Image`) 与**容器** (`Container`) 的关系，与`类`和`实例`类似 - 镜像是静态的定义；容器是镜像运行时的实体。容器可以被创建、启动、停止、删除、暂停等。[[3]](https://yeasy.gitbook.io/docker_practice/basic_concept/container)
### 仓库 (`Repository`)
`Docker Registry` 是一个集中集中的存储和分发镜像的服务。方便在其它服务器上使用构建好的镜像。一个 `Docker Registry` 可以包含多个**仓库** (`Repository`)； 每个仓库可以包含多个**标签** (`Tag`)；每个标签对应一个镜像。

## 常用指令 [[4]](https://yeasy.gitbook.io/docker_practice/image)
### 获取镜像
Docker Hub 上有很多官方的镜像，可以通过类似 GitHub 的操作将这些镜像拉取到本地。不加 `Tag` 默认最新版本。
```
docker pull [options] [Docker_Registry_Address[:port_num]/]Repository[:Tag]
```
下载镜像可用
### 列出镜像
列出已经下载的镜像文件使用这个。这个指令只显示顶层镜像，如果要查看中间层镜像，可以添加 `-a` 参数。
```
docker image ls
```
查看镜像、容器、数据卷所占用的空间。
```
docker system df
```
删除虚悬镜像。
```
docker image prune
```
### 删除本地镜像
使用 `docker image rm` 指令删除本地镜像。
```
docker image rm [options] <image1> [<image2> ...]
```
其中 `<imagen>` 可以是`镜像短 ID`、`镜像长 ID`、`镜像名`或`镜像摘要`。`镜像短 ID` 一般输入`镜像长 ID` 的前三个字符就可以；`镜像名`就是`<仓库名>:<标签>`。
### 新建并启动容器
运行容器可以使用这条指令。
```
docker run [options] <image>:[tag] [command]
eg. docker run -it ubuntu:16.04 /bin/bash
```
- `-i`：交互式操作。
- `-t`：终端。
- `ubuntu:16.04`：指的用 `ubuntu:16.04` 镜像为基础启动容器。
- `/bin/bash`：放在镜像名后的是**命令**，这里是交互式的 Shell，所以用了 `bash`。
- `--name="nginx-lb"`：为容器指定一个名称；
- `-e xxx-env="Hello"`：设置环境变量
- `-v host-path:container-path`：mount主机目录到容器内
- `-p host-port:container-port`：映射主机端口到容器内端口
- `--device`：传递设备
执行后，就进入 `ubuntu:16.04` 系统啦。可以执行 `cat /etc/os-release` 查看系统版本。
### 操作容器
启动已终止容器
```
docker container start <container>
```
终止运行中的容器
```
docker container stop <container>
```
重启容器
```
docker container restart <container>
```
进入容器
```
docker container exec -it <container> /bin/bash
```
退出容器
```
exit
```
### 删除容器
删除目标容器
```
docker container rm <container>
```
清除所有终止态的容器
```
docker container prune
```

## 数据管理 [[5]](https://yeasy.gitbook.io/docker_practice/data_management)
![Figure1. Data Management of Docker](asset/types-of-mounts.png)  
在容器中管理数据有两种方式
- 数据卷 (Volumes)
- 挂载主机目录 (Bind mounts)
### 数据卷
### 挂载主机目录
