## Docker认识 ##
集装箱，便携的虚拟机应用容器，能够在容器内运行任何应用，且两两容器之间互不影响。

## Docker用途 ##
1.环境隔离

2.微服务定制

3.为客户演示，考一个Docker镜像即可。

## Docker应用场景 ##
不同的应用程序有不同的应用环境，使用Docker容器就不会造成应用环境冲突

本地环境/测试环境/生产环境不一样，同样的代码无法运行，使用Docker容器统一环境问题

web应用的自动化打包和发布，自动化测试和持续集成、发布

## Docker使用 ##
Docker搭建，基于centOS7。基于Linux安装Docker，yum安装和curl脚本安装

Dockerfile
配置文件，分为基础镜像/维护者信息/镜像操作/容器启动命令4个部分，使用Dockerfile自动构建镜像

镜像：容器的只读版本，方便存储和交流

CentOS启动Docker

    systemctl start docker
## Docker配置 ##
安装成功后的Docker是“裸”Dokcer

Dokcer拉取tomcat/Ngnix等容器

把容器内的ngnix的80端口映射到8080端口

    docker run -d -p 8080:80 nginx
使用多个Ngnix，如修改80端口映射到8081端口

    docker run -d -p 8081:80 nginx
查看Dokcer容器Id

    docker ps -a
     

部署
 打包SpringBoot项目，打成jar包

        在centOS 7 服务器放置Dockerfile 和jar包

            生成镜像文件，进入本地Docker仓库

    docker build -t docker
            `-t 构建的镜像的tag`
建立端口映射，运行

    docker run -d -p 8080:8080 docker
