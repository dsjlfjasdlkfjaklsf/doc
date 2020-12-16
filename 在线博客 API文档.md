# 在线博客 API文档

## Schema

所有的APi通过HTTPS访问，所有的数据通过JSON的格式传输。

除了用处创建和登录请求之外，通过HTTP header中的token判断本次请求是否有效，如果token有效，那么就按照请求返回资源，如果token无效，则返回对应的错误提示。

正确返回信息的HTTP的状态码都设置为200，返回信息的格式都如下所示：

```c
{
	"state": bool; //true or false 表示是否成功
	"response": json/string //返回的正确or信息，或者请求到的数据
}
```

需要注意的是，前端上传给后端的Password，应该是用户输入的密码哈希后的结果（比如说用MD5哈希），避免进行明文传输，后端存储的也是哈希后的结果。

## HTTP Verbsc

| Verb   | Description                  |
| ------ | ---------------------------- |
| GET    | 用于获取博客内容             |
| POST   | 用于新建博客、用户注册和登录 |
| DELETE | 用于删除博客                 |

## User

### 创建用户 [url:/signup]

```c
method:POST
body:{
	"ID": string, // eg. "32183921@qq.com"
	"Name": string, //eg. "PmlPml"
	"Password": string //eg. 123456加密后的密文
}

//返回值
//创建成功
{
	"state": true, //创建成功
	"response": string //"成功信息"
}
//创建失败
{
	"state":false, //创建失败
	"response": string // 失败信息，比如“已经有相同的ID”，或者”昵称不符合规范等“。
}

```

### 用户登录 [url:/login]

```c
method:POST
body{
	"ID":string,
 	"Password":string   
}
//返回值
//登录成功
{
    "state":true,
    "response":string// 返回值可以是Token，之后页面可以用该Token访问其他数据
}
//登录失败
{
    "state":false,
    "response":string//失败的具体信息
}
```

### 获取登录用户的信息 [url:/{ID}/Inf]

```c
method:Get
body{
	"Token":string //标识身份是否可靠
}
//获取成功
{
	   "state":true,
    	"response":{ //一个json 用户的信息
		 	"ID":"32183921@qq.com",
			“Name”:"PmlPml",
			"Password":"123456"
	}
}
//获取失败
{
    "state":false,
    "response":string//失败的具体信息
}
```

## Blog

### 创建博客 [url/blog]

```c
method:POST
head:{
	"token"
}
body:{
	"title": string,//博客标题
	"abstract": string, //博客的摘要
	"content": string //博客的正文
}

//返回值
//创建成功
{
    "state":true,
    "response": string //创建成功的信息，任意指定
}

//创建失败
{
    "state":false,
    "response": string//创建失败的信息
}
```

### 获取所有博客 [url/blog/all]

```c
//该方法可以不登录获取所有博客
method:GET
head:{}
body:{}

//获取成功
{
	"state":true,
	"response":{
        { //一个json 所有博客的信息
		"BlogID":"dagwewewfcwfedcwe",
		"AuthorID":"32183921@qq.com",
        "AuthorName":"PmlPml",
		"createtime":"2020-12-13 16:25:48",
		"title":"测试文章",
		"abstract":"12312312",
		"content":"hellow world"
		},
        {
           "BlogID":"dagwewewfcwfedcwf",
			"AuthorID":"32183921@qq.com",
        	"AuthorName":"PmlPml",
			"createtime":"2020-12-13 16:25:48",
			"title":"测试文章",
			"abstract":"12312312",
			"content":"hellow world"
		},
    }
}
c
//获取失败
{
	"state":false,
    "response": string//获取失败的提示
}
```

### 获得博客用户所有博客 [url/{ID}/all]

```C
method:GET
head:{
	"token":string 
}
body:{}

//返回值
//申请成功
{
    "state":true,
    "response": { //一个json 样例
		{"BlogID":"dagwewewfcwfedcwe",
		 "AuthorID":"32183921@qq.com",
         "AuthorName":"PmlPml",
		"createtime":"2020-12-13 16:25:48",
		"title":"测试文章,
		"abstract":"12312312"
		"content":"hellow world",
		},
		
		{"BlogID":"dagwewewfcwfedcwe",
		 "AuthorID":"32183921@qq.com",
         "AuthorName":"PmlPml",
		"createtime":"2020-12-13 16:35:21",
		"title":"测试文章,
		"abstract":"12312312"
		"content":"hellow world",
		},
	} 
}

//申请失败
{
	"state":false,
    "response": string//申请失败的提示
}
```

### 获取单个博客的内容[url/blog/{BlogID}]

```c
method: Get
head:{
	"token":string
}
body{}

//返回值
//获取成功
{
	"state":true,
	"response":{ //一个json 单个博客的信息
		"BlogID":"dagwewewfcwfedcwe",
		 "AuthorID":"32183921@qq.com",
        "AuthorName":"PmlPml",
		"createtime":"2020-12-13 16:25:48",
		"title":"测试文章",
		"abstract":"12312312",
		"content":"hellow world"
	}
}

//获取失败
{
	"state":false,
    "response": string//获取失败的提示
}
```

### 删除单个博客 [url/blog/{BlogID}]

```c
method:Delete
head:{
	"token":string
}
body:{
    "BlogID":string //博客ID
}
    
//返回值
//删除成功
{
    "state":true,
    "response": string //删除成功的信息，任意指定
}
//删除失败
{
    "state":false,
    "response": string//删除失败的信息
}
```

## Comment

### 添加评论 [url/comment]

```c
method:POST
head:{}
body:{
	"CommentName": string,//评论人的名字
	"content": string //评论的内容
}
//返回值
//创建成功
{
    "state":true,
    "response": string //评论成功的信息，任意指定
}

//创建失败
{
    "state":false,
    "response": string//评论失败的信息
}
```

### 获取评论 [url/comment/]

```c
method: Get
head:{
	"token":string
}
body{}
//返回值
//获取成功
{
	"state":true,
	"response":{ //一个json 样例
		{"BlogID":"dagwewewfcwfedcwe",
         	  "OwnName":"Hsy", // 评论人的名称
		 "CommentTime":"2020-12-16 16:25:48",
		 "content":"谢谢您的博客，帮助很大",
		},
		{"BlogID":"dagwewewfcwfedcwe",
         	   "ownName":"Xht",
		  "CommentTime":"2020-12-16 16:35:21",
		 "content":"开始有不懂的，现在懂了！",
		},
}
//获取失败
{
	"state":false,
        "response": string//获取失败的提示
}
```



## Tag

### 添加标签 [url/tag/{BlogID}]

```c
method:POST
head:{
	"Token"//验证身份
}
body:{
	"TagName": []string //添加的标签,是一个string的数组，建议最多不超过6个
}
//返回值
//创建成功
{
    "state":true,
    "response": string //添加标签成功的信息，任意指定
}

//创建失败
{
    "state":false,
    "response": string//添加标签失败的信息
}
```



### 获取标签 [url/tag/{BlogID}]

```c
method: Get
head:{
	"token":string
}
body{}
//返回值
//获取成功
{
	"state":true,
	"response": string[] //一个string的数组
}
//获取失败
{
	"state":false,
    "response": string//获取失败的提示
}
```











