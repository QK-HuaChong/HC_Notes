# Doucker

## 1、虚拟机和容器的区别

- 虚拟机：
  >每台虚拟机都需要有自己的操作系统，虚拟机一旦被开启，预分配给它的资源将全部被占用。每一台虚拟机包括应用，必要的二进制和库，以及一个完整的用户操作系统。

- 容器：
  >容器技术是和我们的宿主机共享硬件资源及操作系统，可以实现资源的动态分配。

## 2、Docker的优点：

- 更快速的交付和部署
- 高效的部署和扩容
- 更高的资源利用率
- 更简单的管理

## 3、Docker引擎：

- Server是一个常驻进程
- REST API 实现了client和server间的交互协议
- CLI 实现容器和镜像的管理，为用户提供统一的操作界面
![Docker引擎](img/engine-components-flow.png)

## 4、Docker构架

![Docker框架](img/architecture.jpg)

### 4.1、核心概念

- 镜像
  >Docker 镜像（Image）就是一个只读的模板。除了提供容器运行时所需的程序、库、资源、配置等文件外，还包含了一些为运行时准备的一些配置参数(如匿名卷、环境变量、用户等)。
- 仓库
  >仓库（Repository）是集中存放镜像文件的场所。
- 容器
  >容器的定义和镜像几乎一模一样，也是一堆层的统一视角，唯一区别在于容器的最上面那一层是可读可写的。

## Docker 安装部署

[Docker下载地址](https://www.docker.com/products/container-runtime)

### Docker 常用命令

获取镜像

>docker pull 镜像名称（centos:centos6）

查看镜像列表
  
>docker images

利用Dockerfile创建镜像

- 创建一个 Dockerfile
  
    ```cmd
    mkdir hainiu
    cd hainiu
    touch Dockerfile
    ```

>docker build

上传镜像

>docker push

创建容器
  
>docker create \<image-id>

启动容器

>docker start \<container-id>

进入容器

>docker exec \<container-id>

停止容器

>docker stop \<container-id>

删除容器

>docker rm \<container-id>

运行容器

>docker run \<container-id>

查看容器列表

>docker ps

删除镜像

>docker rmi \<image-id>

提交容器

>docker commit \<container-id>

保存镜像

>docker save \<image-id>

容器导出

>docker export \<container-id>
