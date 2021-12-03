- 📖*Github用户如果访问速度慢的话，点击[在线阅读](https://wangcongbirley.gitee.io/sjg/)*

<p align="center">
<a href="https://github.com/wangcongbirley/Senior-Java-Guide" target="_blank">
	<img src="./images/logo.png" width="20%" />
</a>
</p>

<p align="center">
  <a href=""><img src="https://img.shields.io/badge/阅读-read-brightgreen.svg" alt="阅读"></a>
  <a href="#投稿"><img src="https://img.shields.io/badge/support-投稿-critical.svg" alt="投稿"></a>
</p>

<h1 align="center">Java-Home</h1>

> ☕ **Java-Home** 是一个 Java 核心技术及实践教程，从头搭建可承载高并发量访问的系统。
## 目录 ☕ 
- [系统设计](#系统设计)
    - [系统整体设计](#系统整体设计)
    - [框架篇](#框架篇)
        - [Spring](#spring)
        - [SpringBoot](#springboot)
        - [SpringMVC](#springmvc)
        - [MyBatis](#mybatis)
    - [微服务](#微服务)
       - [项目架构](#项目架构)
       - [技术栈选型](#技术栈选型)
       - [网关层](#网关层)
       - [注册中心](#注册中心)
       - [nacos](#nacos)  
       - [治理策略](#治理策略)
       - [运维服务层](#运维服务层)
       - [系统监控](#系统监控)    
       - [部署](#部署)
           - [Docker](#Docker)
           - [tomcat集群](#tomcat集群)
    - [消息队列](#消息队列)
    - [分布式](#分布式)
        - [Elasticsearch](#elasticsearch)
        - [消息队列](#消息队列)
        - [API 网关](#api-网关)
        - [唯一 id 生成](#唯一-id-生成)
        - [数据库扩展](#数据库扩展)
    - [高并发](#大型网站架构)
        - [高并发](#高并发)
        - [高可用](#高可用)
- [工具篇](#工具篇)
    - [Linux](#linux)
    - [Docker](#docker)
    - [Maven](#maven)
- [其他](#其他)
    - [jvm原理](#jvm原理)
    - [java并发](#并发)
- [说明](#说明)

业务场景是验证架构合理性的标准之一。

## 系统设计

#### 系统整体设计

- [系统架构方案](docs/microservice/systemdesign.md)

### 框架篇

#### Spring

1. [Spring 学习与面试](docs/spring/spring.md)

2. [Spring AOP介绍](docs/spring/springaop.md)

#### SpringBoot

- [SpringBoot 指南](docs/microservice/springboot.md)

- [SpringBoot启动原理分析](docs/microservice/springboot-starter.md)

- [Spring 所有注解及使用方法](docs/microservice/springannotation.md)


#### SpringMVC
- [SpringMVC 工作原理详解](docs/spring/springmvc.md)

#### MyBatis

- [MyBatis常见问题总结](docs/orm/mybatis.md)

### 微服务

自顶向下设计微服务平台，以下是系统设计过程。

### 项目架构
系统分层，用户、接入层、网关层、业务服务层、基础服务层、运维服务层。分层目的是松耦合，增加拓展性。架构图如下
![](/images/1.png)

前端使用vue/element-ui构建可视界面，后端采用maven多模块/springboot构建API接口，业务层。项目通过华为his部署，灰度发布。
#### 技术栈选型

1. [微服务技术栈有哪些？](docs/micro-stack.md)

### 网关层
网关应用，提供网关路由转发、降级、熔断、请求处理等网关功能。
gateway-admin 提供路由应用管理，包括路由配置，设置灰度分流。
网关主要做了一件事：请求过滤。我们在网关处理一些非业务逻辑的事情，权限认证、缓存、请求路由等。
#### 常用开源网关组件
- Kong
- zuul

#### API网关
使用API中心订阅机制。

### 注册中心
- Zookeeper
- nacos
- euraka

#### nacos
使用nacos替代eureka为服务的注册中心。

1. [SpringCloud Euraka](docs/springcloud.md)


#### 治理策略

1. [治理策略](docs/micro-governance.md)


#### redis

1. [redis](docs/redis.md)


### 运维服务层

#### 系统监控

监控数据埋码，公共js植入自动采集代码，每个页面挂载函数中添加埋码。

1. [Kibana](docs/kibana.md)

2. [druid](docs/druid.md)
### 跳板机
使用jumper连接远程桌面、linux主机。

#### 部署

部署发布使用华为鲲鹏计算云，RDS的MySQL集群，灰度发布。项目打成war包，使用tomcat集群。生产环境操作需提交变更号，经过专家评审，审批通过后部署。

1. [部署模式](docs/micro-deployment.md)
2. [tomcat集群](docs/deploy.md)

##### Docker
Docker是一个开源的容器引擎，它有助于更快地交付应用。方便快捷已经是 Docker的最大优势，过去需要用数天乃至数周的任务，在Docker容器的处理下，只需要数秒就能完成。

Docker-compose 是 docker 提供的一个命令行工具，用来定义和运行由多个容器组成的应用。使用 compose，我们可以通过 YAML 文件声明式的定义应用程序的各个服务，并由单个命令完成应用的创建和启动。

##### docker部署系统
提前准备发布计划，线上BUG的回滚和修复计划

本地部署好自己的服务->生产或测试部署服务->导出镜像，变成tar.gz压缩包->生产或测试解压压缩包->导入（load）镜像->开一个容器，启动

使用 docker-comose.yml，Dockerfile初始化 

service   定义服务名称     image：镜像名称     container_name：自定义项目名称
如果需要构建：使用build标签三级标签：depends_on 依赖

```
  depends_on:  
  	- db   
  	- redis 
  redis:  
  	image: redis 
  db:  
  	image: postgres
```

###### 标签含义

environment：环境变量

external_links：连接在compose.yml外部的容器 

links：创建连接到其他服务中的容器

extra_hosts：修改hosts文件

logging：配置日志服务，options可选值

ports：映射端口的标签

volumes：挂在数据卷
##### tomcat集群
-[tomcat集群](docs/deploy.md)

#### 缓存
- [为什么使用redis？redis使用不当会造成哪些后果](docs/cache/redis.md)

### 分布式

#### elasticsearch

- [elasticsearch简介](docs/microservice/elasticsearch.md)

#### 消息队列
1. [消息队列选型](docs/mq.md)

## 工具篇
### Linux
- [linux命令](docs/microservice/linux.md)

### Docker

- [Docker 解读](docs/microservice/Docker.md)

### Maven

maven在主流开发中是非常常用的。

- [Maven 模块](docs/orm/maven.md)

## 其他
### jvm原理
- [jvm内存模型和垃圾回收](docs/basic/JVM.md)

### 并发
- [多线程并发及juc包](docs/basic/concurrent.md)

### java基础
- [异常](docs/basic/java.md)

## 说明📚

Markdown 格式参考：[Github Markdown格式](https://guides.github.com/features/mastering-markdown/)，表情素材来自：[EMOJI CHEAT SHEET](https://www.webpagefx.com/tools/emoji-cheat-sheet/)。

利用 docsify 生成文档部署在 Github pages: [docsify 官网介绍](https://docsify.js.org/#/)


## 学习资源 💎

- **书籍**
  - Java 四大名著
    - [《Java 编程思想（Thinking in java）》](https://item.jd.com/10058164.html)
    - [《Java 核心技术 卷 I 基础知识》](https://item.jd.com/12759308.html)
    - [《Java 核心技术 卷 II 高级特性》](https://item.jd.com/12791368.html)
    - [《Effective Java》](https://item.jd.com/12507084.html)
  - Java 并发
    - [《Java 并发编程实战》](https://item.jd.com/10922250.html)
    - [《Java 并发编程的艺术》](https://item.jd.com/11740734.html)
  - Java 虚拟机
    - [《深入理解 Java 虚拟机》](https://item.jd.com/11252778.html)
  - Java 入门
    - [《O'Reilly：Head First Java》](https://item.jd.com/10100190.html)
    - [《Java 从入门到精通》](https://item.jd.com/12555860.html)
    - [《疯狂 Java 讲义》](https://item.jd.com/12518025.html)
  - 其他
    - [《 Java 网络编程》](https://item.jd.com/11544991.html)
    - [《Java 加密与解密的艺术》](https://item.jd.com/26122568270.html)
    - [《Java 程序员面试宝典》](https://item.jd.com/11772823.html)
- **教程、社区**
  - [Runoob Java 教程](https://www.runoob.com/java/java-tutorial.html)
  - [JavaGuide](https://github.com/Snailclimb/JavaGuide)
  - [Java](https://github.com/TheAlgorithms/Java)
  - [java-design-patterns](https://github.com/iluwatar/java-design-patterns)
  - [advanced-java](https://github.com/doocs/advanced-java)
