### maven多模块设计，图示如下
![](/images/maven-1.png)

### maven模块和各组件的依赖关系
![](/images/maven-2.png)

## maven作为依赖包管理工具，广泛运用于企业级开发中。
#### maven根元素含义及用法

#### maven本地仓库
 配置setting.xml，设置国内镜像。
    公司使用云龙仓库，可选阿里云仓库。

#### 多模块配置

子模块
`<packaging>jar</packaging>`
父模块
`<packaging>war</packaging>`
根模块
`<packaging>pom</packaging>`

子模块相互调用，打jar包，其他模块添加依赖后调用。
