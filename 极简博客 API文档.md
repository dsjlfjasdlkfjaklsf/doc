# 极简博客 API设计

本次项目的API设计参考的是`Github V3`，参考的博客是[Github API v3 介绍文档](https://www.cnblogs.com/chen-xing/p/github_api_v3.html)

## HTTP Verbsc

| Verb   | Description                  |
| ------ | ---------------------------- |
| GET    | 用于获取博客内容             |
| POST   | 用于新建博客、用户注册和登录 |
| DELETE | 用于删除博客                 |

## 设计概览

本次项目涉及的API一共包括四类，一共是13个APi，分别如下

| API种类 | url                 | method | 功能                     |
| ------- | ------------------- | ------ | ------------------------ |
| Blog    | /blog               | POST   | 添加一个新的博客         |
|         | /blogs              | GET    | 获取所有的公开博客       |
|         | /blogs/{UserID}     | GET    | 获取某一个用户的博客     |
|         | /blog/{BlogID}      | GET    | 获取某个博客的具体信息   |
|         | /blog/{BlogID}      | DELETE | 删除某一个具体的博客     |
| User    | /user/signup        | POST   | 用户注册                 |
|         | /user/login         | POST   | 用户登录                 |
|         | /user/logout        | GET    | 用户登出                 |
|         | /user/{UserID}/info | GET    | 获取某一个用户的具体信息 |
| Comment | /comment/{BlogID}   | POST   | 发送评论                 |
|         | /comment/{BlogID}   | GET    | 获取博客评论             |
| Tag     | /tag/{BlogID}       | GET    | 获取博客标签             |
|         | /tag/{BlogID}       | POST   | 给博客添加标签           |

## Schema

> 所有的api访问都必须是是通过https和后端服务器，所有的数据发送和接受都是JSON格式的。

以下是设计的一个成功获取信息的返回的JSON的例子。

```c
{
  "state": true,//true表示获取成功，false表示获取失败
  "response": "success"//描述成功/失败的信息
}


```

以下是本次实验涉及到的所有Schema

![3](https://gitee.com/xinghanting/image/raw/master/ServiceComputing/homework9/3.png)

## API实例

完整的API可以查看 [A Blog System](https://app.swaggerhub.com/apis-docs/CSBlog/a-blog_system/1.0.0#/)，本次项目使用了`SwaggerHub`存放项目的API，方便前后端进行使用，以下是按照项目要求模仿 [GitHub Docs](https://docs.github.com/en/free-pro-team@latest/rest/reference/actions) 撰写的几个API的实例。

### Add a new Blog

Post a new blog after logining. Only the user can use this.

#### Parameters

| Name       | Type   | In    | Description                                           |
| :--------- | :----- | :---- | :---------------------------------------------------- |
| `Title`    | string | query | The title of the blog                                 |
| `Abstract` | string | path  | The abstract of the blog                              |
| `ID`       | string | path  | The ID of user that you want to get information from. |

#### Default response

```
Status: 200 OK
```

```c
{
  "state": true,
  "response": "success"
}
```

### Get User Information

Get User Information. After logining, user can use this API for geting information of yourself.

```
GET /user/{ID}/info
```

#### Parameters

| Name | Type   | In   | Description                                           |
| :--- | :----- | :--- | :---------------------------------------------------- |
| `ID` | string | path | The ID of user that you want to get information from. |

#### Default response

```
Status: 200 OK
```

```c
{
  "state": true,
  "response": {
    "ID": "32183921@qq.com",
    "Name": "PmlPml",
    "Bio": "好好学习天天向上",
    "Level": 1
  }
}
```

### Get Comment of a blog

#### Parameters

| Name      | Type   | In    | Description                |
| :-------- | :----- | :---- | :------------------------- |
| `BlogID`  | string | query | The IDof the blog          |
| `ownName` | string | path  | path                       |
| `content` | string | path  | The content of the comment |

#### Default response

```
Status: 200 OK
```

```c
{
  "state": true,
  "response": "success"
}
```

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







