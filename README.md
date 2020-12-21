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
| 黄绍永 |          |                                   |
|        |          |                                   |
|        |          |                                   |
|        |          |                                   |
| 徐浩添 | 18342109 | 设计博客所需API，编写项目使用文档 |

## 个人报告



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