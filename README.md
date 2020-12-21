# 服务计算小组作业 简单Web服务

## 项目简介

项目名称：极简博客

项目目标：

1. 选择合适的 API，实现从接口或资源（领域）建模，到 API 设计的过程
2. 使用 API 工具，编制 API 描述文件，编译生成服务器、客户端原型
3. 使用`Github`建立一个组织（[点击查看](https://github.com/dsjlfjasdlkfjaklsf)），通过 API 文档（[点击查看](https://app.swaggerhub.com/apis-docs/CSBlog/a-blog_system/1.0.0)），实现客户端项目与RESTful 服务项目同步开发
4. 使用 API 设计工具提供 Mock 服务，两个团队独立测试 API
5. 使用`travis`测试相关模块

## 项目要求

| 项目要求               | 完成说明                                 |
| ---------------------- | ---------------------------------------- |
| 开发周期               | 2000年12月7日 - 2000年12月21日           |
| 每个项目仓库的介绍文档 | 查看各个仓库的README，有各仓库的使用介绍 |
| 客户界面与美术         | 查看web仓库                              |
| API设计                | 查看doc仓库`极简博客 API设计`            |
| 资源来源               | 手动抓取CSDN上博客，存放在doc仓库        |
| 服务器端数据库支持     | 支持MongoDB                              |
| 页面数与API限制        | 页面数： API个数：4类13个                |
| API要求                | 查看本篇文章 `API使用说明`               |
| 加分项                 | 有四个API支持Token（带锁的就是支持的）   |

## 项目分工

| 姓名   | 学号     | 分工说明                          |
| ------ | -------- | --------------------------------- |
| 黄绍永 | 18342030 | 搭建前后端脚手架，配置后端数据库     |
| 何泽豪 | 17345021 | 前端登录页，注册页，主页，博客管理页设计开发  |
|   李浩 | 18342045 |       博客页面，创建博客    |
| 徐浩添 | 18342109 | 设计博客所需API，编写项目使用文档 |

## 个人报告

[18342030-黄绍永](./黄绍永.md)

[17345021-何泽豪](./何泽豪.md)

[18342045-李浩](./李浩.md)

[18342109 徐浩添](./徐浩添.md)



## 仓库说明

`go-server` 存放了本次项目的后端代码

`web` 存放了本次项目的前端代码

`doc` 存放了本次项目使用的API、测试数据，以及项目文档与个人报告

## API页面使用说明

本仓库的使用的是`go module`管理项目依赖，如果开启可以根据以下的步骤开启。

在系统变量中新增两个属性（在命令行中修改只是暂时的，所以需要在系统环境变量中修改）：

> `GO111MODULE=on`
> `GOPROXY=https://goproxy.io`

使用`go env`查看是否修改成功。

环境配置完成之后，可以直接运行本仓库的`main.go`

```go
go run main.go
```

`main.go` 是使用了`gin-swagger`，将本地写好的`yaml`文档，渲染成一个静态的网页，方便进行查询。本地运行服务器之后，在浏览器输入

`http://localhost:8080/swagger/index.html`

可以看到渲染好的静态页面，如下：

![1](https://gitee.com/xinghanting/image/raw/master/ServiceComputing/homework9/1.png)

其中，我已经使用`swaggerHub`注入了一些调用的返回值的例子，所以这个静态页面中的API是可以调用的，执行其中一个API的结果如图：

![2](https://gitee.com/xinghanting/image/raw/master/ServiceComputing/homework9/2.png)

## 项目运行样例

在按照

[Go Server for our Blog System](https://github.com/dsjlfjasdlkfjaklsf/go-server)

[blog-web](https://github.com/dsjlfjasdlkfjaklsf/web)

配置好了之后，就可以访问`localhost:8000`查看本次项目运行的结果了。

首先进入的是登录页面

![4](https://gitee.com/xinghanting/image/raw/master/ServiceComputing/homework9/4.png)

点击注册按钮，可以跳转到注册页面

![5](https://gitee.com/xinghanting/image/raw/master/ServiceComputing/homework9/5.png)

登录之后，进入的是`public Blog`页面，在这个页面可以查看所有人发布的博客。

![6](https://gitee.com/xinghanting/image/raw/master/ServiceComputing/homework9/6.png)

这里面的博客是之前学习的区块链的资料，发布在[CSDN](https://blog.csdn.net/lianquan_cn/article/details/81565638)上，是公开的信息。

点击查看按钮，可以跳转到查看该博客的页面

![7](https://gitee.com/xinghanting/image/raw/master/ServiceComputing/homework9/7.png)

![8](https://gitee.com/xinghanting/image/raw/master/ServiceComputing/homework9/8.png)

在博客的最下面，可以发布评论。

也可以自己发布博客，分别是标题、摘要和正文

![9](https://gitee.com/xinghanting/image/raw/master/ServiceComputing/homework9/9.png)

最后发布成功的结果会显示出来

![10](https://gitee.com/xinghanting/image/raw/master/ServiceComputing/homework9/10.png)

这就是本次项目运行的大致成果，更多细节可以在本机上运行代码。