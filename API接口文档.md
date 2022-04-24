# API 接口文档统一说明

* 接口基准地址：
* * PC端：http://localhost:8881/api/
  * 后台：http://localhost:8881/admin/
* 服务端未开启CORS跨域请求
* 数据返回格式统一使用JSON



# PC端 API 接口文档

## 一、留言

### 1.发表留言接口

* 请求路径：/comment/create
* 请求方式：post
* 请求参数：

| 参数名     | 参数说明         | 备注                     |
| ---------- | ---------------- | ------------------------ |
| name       | 留言者输入的昵称 | 不能为空                 |
| createTime | 留言的时间       | 格式：2022-4-24 10:27:00 |
| note       | 留言的内容       | 不能为空                 |

* 响应参数

* 响应数据

```json
{
    "meta": {
        "message": "留言成功！",
        "status": 200
    }
}
```



### 2.点赞接口

* 请求路径：/comment/givelike
* 请求方式：post
* 请求参数

| 参数名    | 参数说明         | 备注       |
| --------- | ---------------- | ---------- |
| ifTrue    | 点赞还是取消点赞 | true为点赞 |
| commentId | 留言的id         |            |

* 响应参数
* 响应数据

```json
{
    "meta": {
        "message": "点赞成功！",
        "status": 200
    }
}
```



### 3.获取留言接口

* 请求路径：/comment/getcomments
* 请求方式：get
* 请求参数：无
* 响应参数

| 参数名      | 参数说明           | 备注 |
| ----------- | ------------------ | ---- |
| id          | 留言在数据库中的id |      |
| com_name    | 留言者的昵称       |      |
| create_time | 留言时间           |      |
| good_number | 点赞数             |      |
| com_content | 留言内容           |      |

* 响应数据

```json
{
    "data": [
        {
            "id": 72,
            "com_name": "fasd f",
            "create_time": "2022-04-24T10:50:21.000Z",
            "good_number": 7,
            "com_content": "fas dsf "
        },
        ......
        {
            "id": 63,
            "com_name": "萨芬",
            "create_time": "2022-04-21T14:49:52.000Z",
            "good_number": 0,
            "com_content": "飞洒"
        }
    ],
    "meta": {
        "message": "获取了前10条评论！",
        "status": 200
    }
}
```







# 后台 API 接口文档

## 一、登录

### 1.登录接口

* 请求路径：/
* 请求方式：post
* 请求参数：

| 参数名   | 参数说明 | 备注 |
| -------- | -------- | ---- |
| name     | 用户名   |      |
| password | 用户密码 |      |

* 响应参数

| 参数名 | 参数说明              | 备注                           |
| ------ | --------------------- | ------------------------------ |
| code   | 表示是否登录          | 0表示允许登录，1表示不允许登录 |
| token  | 登录成功后颁发的token |                                |

* 响应数据

```json
{
    "data": {
        "code": 0,
        "token": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiYWRtaW4iLCJwYXNzd29yZCI6InQxODU4MTc2NjEwNCIsImlhdCI6MTY1MDc4MDE4NiwiZXhwIjoxNjUwODY2NTg2fQ.pyrbLnyCW0kT9iVDq-qCPowyR_b-l-2SIcoAcp_UtZL_ptwLRXrFTQznI9C26pU8ibbd9AGxAP3392064FDKN3aU5ohd6sLgZKEQna71_HAVrrlpGCmLXXEnRAfaPHAvGue7j197Rs3GRP1qFtYHqTFdphe8vU3goWT0Vke0R-E"
    },
    "meta": {
        "message": "登录成功！",
        "status": 200
    }
}
```



## 二、笔记

### 1.获取笔记分类接口

* 请求路径：/getsortlist
* 请求方式：get
* 请求参数：无
* 响应参数：

| 参数名    | 参数说明     | 备注 |
| --------- | ------------ | ---- |
| sortArray | 笔记分类列表 | 数组 |

* 响应数据

```json
{
    "data": {
        "sortArray": [
            "vue",
            "other",
            "node",
            "mysql",
            "javascript",
            "issue",
            "css"
        ]
    },
    "meta": {
        "message": "获取分类列表成功！",
        "status": 200
    }
}
```

### 2.上传笔记接口

* 请求路径：/uploadnote
* 请求方式：post
* 请求参数：

| 参数名     | 参数说明 | 备注                     |
| ---------- | -------- | ------------------------ |
| title      | 笔记标题 |                          |
| describe   | 笔记描述 |                          |
| content    | 笔记内容 |                          |
| sort       | 笔记分类 | 只能选择已有的分类       |
| createtime | 上传时间 | 格式：2022-4-24 10:27:00 |

* 响应参数：

| 参数名 | 参数说明     | 备注             |
| ------ | ------------ | ---------------- |
| code   | 是否上传成功 | 0：成功，1：失败 |

* 响应数据

```javascript
{
    "data": 0,
    "meta": {
        "message": "上传成功！",
        "status": 200
    }
}
```

