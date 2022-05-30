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





## 二、笔记

### 1.获取笔记分类接口

* 请求路径：/notes/getsortlist
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

### 2.根据分类获取笔记

* 请求参数：/notes/getsomenote
* 请求方式：post
* 请求参数

| 参数名 | 参数说明 | 备注             |
| ------ | -------- | ---------------- |
| sort   | 笔记分类 | 数据库中已有类型 |

* 响应参数：

| 参数名 | 参数说明     | 备注     |
| ------ | ------------ | -------- |
| notes  | 查询到的笔记 | 数组类型 |

* 响应数据：

```json
{
    "data": {
        "notes": [
            {
                "id": 63,
                "note_title": "vue基础",
                "note_describe": "主要包括vue的初始化、指令、生命周期等知识点。",
                "note_content": "asf",
                "note_createtime": "2022-04-24T16:51:00.000Z",
                "note_sort": "vue"
            },
            .......
        ]
    },
    "meta": {
        "message": "获取成功！",
        "status": 200
    }
}
```

### 3.根据id获取笔记内容

* 请求路径：/notes/getnotecontent
* 请求方式：post
* 请求参数：

| 参数名 | 参数说明 | 备注 |
| ------ | -------- | ---- |
| noteId | 笔记的id |      |

* 响应参数：

| 参数名  | 参数说明 | 备注             |
| ------- | -------- | ---------------- |
| content | 笔记内容 | 转为html后的笔记 |

* 响应数据：

```json
{
    "data": {
        "content": "<h2>移动端</h2>\n<h3>一、视口</h3>\n<blockquote>\n<p>视口(viewport)就是浏览器显示页面内容的屏幕区域。</p>\n</blockquote>\n<ul>\n<li>布局视口 layout viewport</li>\n<li>视觉视口 visual viewport</li>\n<li>理想视口 ideal viewport    （meta视口）</li>\n</ul>\n<p><strong>meta视口：</strong></p>\n<blockquote>\n<p>布局视口的宽度应该与理想视口的宽度一致，简单理解就是设备有多宽，我们布局视口就多宽。...."
    },
    "meta": {
        "message": "查询成功",
        "status": 200
    }
}
```

### 4.获取一定数量的笔记接口

> 通过携带的值不同，请求携带的笔记数据不同。

* 请求路径：/notes/getallnote
* 请求方式：post
* 请求参数：

| 参数名 | 参数说明             | 备注              |
| ------ | -------------------- | ----------------- |
| number | 需要获得的笔记信息数 | 传入0表示获得所有 |

* 响应参数：

| 参数名  | 参数说明   | 备注     |
| ------- | ---------- | -------- |
| content | 笔记的信息 | 数组格式 |

* 响应数据

```json
{
    "data": {
        "content": [
            {
                "id": 84,
                "note_title": "的萨芬",
                "note_describe": "十大发s",
                "note_createtime": "2022-04-27T20:24:02.000Z",
                "note_sort": "javascript"
            },
            ...
        ]
    },
    "meta": {
        "message": "获取成功！",
        "status": 200
    }
}
```

## 三、个人介绍

### 1.获取个人信息

> 严格根据请求参数返回查询结果。

* 请求路径：/introduce/getintroduce
* 请求方式：post
* 请求参数：

| 参数名   | 参数说明             | 备注                              |
| -------- | -------------------- | --------------------------------- |
| queryKey | 需要查询的信息内容荣 | 参数内容为”all“时表示查询所有内容 |

* 参数值

| 值              | 说明                  |
| --------------- | --------------------- |
| my_id           | id                    |
| my_name         | 姓名                  |
| my_phone        | 电话                  |
| my_sex          | 性别                  |
| my_email        | 邮箱                  |
| my_birthday     | 生日 格式：2022.02.22 |
| my_qq           | qq号                  |
| my_address      | 地址                  |
| my_koseki       | 户籍                  |
| my_education    | 学历                  |
| my_school       | 学校                  |
| my_professional | 专业                  |
| my_state        | 状态                  |
| my_signature    | 签名 （段落）         |
| my_hobbyies     | 爱好 （段落）         |

* 响应参数：和上面参数值相同

* 响应数据：

```json
{
    "my_id": 1,
    "my_name": "陶继鑫",
    "my_phone": "18581766104",
    "my_sex": "男",
    "my_email": "491675919@qq.com",
    "my_birthday": "2001.07.24",
    "my_qq": "491675919",
    "my_address": "四川省资阳市",
    "my_koseki": "四川省资阳市",
    "my_education": "本科",
    "my_school": "四川工商学院",
    "my_professional": "软件工程",
    "my_state": "学生就读",
    "my_signature": "如果debugging是一种消灭bug的过程，那编程就一定是把bug放进去的过程。",
    "my_hobbyies": "吃饭睡觉打豆豆！"
}
```



## 四、Demo

### 1.获取demo相关信息

* 请求路径：/getalldemo
* 请求方式：post
* 请求参数：

| 参数名 | 参数说明                                         | 备注 |
| ------ | ------------------------------------------------ | ---- |
| getId  | 当值为了值表示查询所有，当为某个值时查询对应信息 |      |

* 响应参数：为一个数组，数组中有多个对象，对象中含对应参数

| 参数名          | 参数说明 | 备注             |
| --------------- | -------- | ---------------- |
| id              | demo的id |                  |
| user_id         |          |                  |
| demo_describe   | 描述     |                  |
| demo_knowkedge  | 知识点   |                  |
| demo_code       | 代码     | 转化为html之后的 |
| demo_createtime | 上传时间 |                  |

* 响应参数：

```json
[
    {
        "id": 1,
        "user_id": 1,
        "demo_describe": "简约动态标签",
        "demo_knowkedge": "transform:rotate、translate，opacity，transition",
        "demo_code": "<p>null</p>\n",
        "demo_createtime": "2022-05-22T16:51:00.000Z"
    },
    ······
    {
        "id": 13,
        "user_id": 1,
        "demo_describe": "简约CSS特效标签",
        "demo_knowkedge": "文字阴影text-shadow",
        "demo_code": "<pre><code class=\"language-javascript\">&lt;template&gt;\n  &lt;div class=&quot;tag&quot;&gt;\n    &lt;div c    ······    }\n\n\n\n}\n&lt;/style&gt;\n</code></pre>\n",
        "demo_createtime": "2022-05-25T15:47:53.000Z"
    }
]
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

### 3.获取所有笔记接口

> 不含笔记内容。

* 请求路径：/getallnote
* 请求方式：post
* 请求参数：无
* 响应参数：

| 参数名          | 参数说明       | 备注                       |
| --------------- | -------------- | -------------------------- |
| id              | 在数据库中的id |                            |
| note_title      | 标题           |                            |
| note_describe   | 笔记描述       |                            |
| note_createtime | 笔记上传时间   | "2022-04-24T16:51:00.000Z" |
| note_sort       | 笔记分类       |                            |

* 响应数据：

```json
[
    {
        "id": 1,
        "note_title": "vue基础",
        "note_describe": "主要包括vue的初始化、指令、生命周期等知识点。",
        "note_createtime": "2022-04-24T16:51:00.000Z",
        "note_sort": "vue"
    },
    ......
    {
        "id": 2,
        "note_title": "dfads",
        "note_describe": "fsdaf",
        "note_createtime": "2022-04-24T21:16:31.000Z",
        "note_sort": "node"
    }
]
```

### 4.按页查询笔记

> 不含内容。

* 请求路径：/getsomenote
* 请求方式：post
* 请求参数：

| 参数名    | 参数说明     | 备注 |
| --------- | ------------ | ---- |
| note_page | 第几页，页数 |      |
| note_num  | 一页条数     |      |

* 响应参数：与获取笔记接口响应参数相同

* 响应数据：与获取笔记接口响应数据相同

### 5.删除笔记

> 根据id删除笔记。

* 请求路径：/deletenote
* 请求方式：delete
* 请求参数：

| 参数名 | 参数说明 | 备注             |
| ------ | -------- | ---------------- |
| id     | 笔记id   | 数据库中的序列号 |

* 响应参数
* 响应数据：

```json
{
    "meta": {
        "message": "删除失败！",
        "status": 500
    }
}
```

### 6.获取某个笔记信息

* 请求路径：/getonenote

* 请求方式：post
* 请求参数：

| 参数名 | 参数说明 | 备注 |
| ------ | -------- | ---- |
| noteId | 笔记id   |      |

* 响应参数：

| 参数名          | 参数说明 | 备注             |
| --------------- | -------- | ---------------- |
| id              | id       |                  |
| note_title      | 标题     |                  |
| note_describe   | 描述     |                  |
| note_content    | 内容     | 转化为html之后的 |
| note_createtime | 上传时间 |                  |
| note_sort       | 分类     |                  |

* 响应数据

```json
{
    "id": 79,
    "note_title": "CSS3",
    "note_describe": "包含CSS3动画以及2D3D转换等内容。",
    "note_content": "## 2D转换\n\n> **转换**（transform）是CSS3中具有颠覆性    ······    </div>\n\t\t</section>\n\t</body>\n</html>\n\n```\n\n",
    "note_createtime": "2022-04-27T19:55:38.000Z",
    "note_sort": "css"
}
```

### 7.修改某个笔记信息

> 根据id修改某个信息。

* 请求参数：/modifynote
* 请求方式：post
* 请求参数：

| 参数名        | 参数说明 | 备注     |
| ------------- | -------- | -------- |
| id            | 笔记id   |          |
| note_title    | 标题     |          |
| note_describe | 描述     |          |
| note_content  | 内容     |          |
| note_sort     | 分类     | 分类固定 |

* 响应参数
* 响应数据

```javascript
"修改成功"
```





## 三、Demo

### 1.获取demo相关信息

> 根据id查询demo相关信息。

* 请求路径：/getdemo
* 请求方式：get
* 请求参数：

| 参数名 | 参数说明               | 备注                             |
| ------ | ---------------------- | -------------------------------- |
| getId  | 需要获取的demo信息的id | getId为0时表示获取所有的demo信息 |

* 响应参数

| 参数名          | 参数说明               | 备注                           |
| --------------- | ---------------------- | ------------------------------ |
| id              | demo信息在数据库中的id |                                |
| user_id         | 用户id                 |                                |
| demo_describe   | demo表述               |                                |
| demo_knowledge  | demo知识点             |                                |
| demo_code       | demo代码               | 格式为html，有markdown转换来到 |
| demo_createtime | 时间                   |                                |

* 响应数据

```json
[
    {
        "id": 12,
        "user_id": 1,
        "demo_describe": "代码片段",
        "demo_knowkedge": "markdoq、html、css",
        "demo_code": "<pre><code class=\"language-javascript\">const { getPassword } = require('../service/login.service')\nconst jwt = require('jsonwebtoken')\nconst { PRIVATE_KEY } = require('../app/config')\nclass LoginController {\n  // 登录\n  async login(req, res, next) {\n    const { name, password } = req.body\n\n    if (password === await getPassword(name)) {\n      // 生成token\n      const token = jwt.sign({ name, password }, PRIVATE_KEY, {\n        expiresIn: 60 * 60 * 24, // 一天\n        algorithm: &quot;RS256&quot; // 这里必须写RS256(非对象加密)，因为默认为HS256(对称加密)\n      })\n      return res.json({\n        data: { code: 0, token: token },\n        meta: { message: &quot;登录成功！&quot;, status: 200 }\n      })\n    }\n\n  }\n}\n\nmodule.exports = new LoginController();\n</code></pre>\n",
        "demo_createtime": "2022-05-25T14:51:02.000Z",
        "path": "dfsdf"
    }
]
```

### 2.添加demo相关信息

* 请求路径：/adddemo
* 请求方式：post
* 请求参数：

| 参数名    | 参数说明 | 备注 |
| --------- | -------- | ---- |
| id        | 用户id   |      |
| describe  | 同上     |      |
| knowledge | 同上     |      |
| code      | 同上     |      |
| time      | 添加时间 |      |
| path      | 路径     |      |

* 响应参数
* 响应数据

```
"添加成功!"
```

### 3.删除demo相关信息

* 请求路径：/deledemo
* 请求方式：delete
* 请求参数：

| 参数名 | 参数说明         | 备注 |
| ------ | ---------------- | ---- |
| demoId | 要删除的demo的id |      |

* 响应参数

* 响应数据

```
"删除成功！"
```

### 4.修改demo相关信息

* 请求路径：/modifydemo
* 请求方式：post
* 请求参数：

| 参数名         | 参数说明 | 备注 |
| -------------- | -------- | ---- |
| demoId         | demo的id |      |
| demo_describe  |          |      |
| demo_knowledge |          |      |
| demo_code      |          |      |
| path           | 路径     |      |

* 响应参数
* 响应数据

```
"修改成功"
```



## 四、个人介绍

### 1.获取个人信息

> 严格根据请求参数返回查询结果。

* 请求路径：/getintroduce
* 请求方式：post
* 请求参数：

| 参数名   | 参数说明             | 备注                              |
| -------- | -------------------- | --------------------------------- |
| queryKey | 需要查询的信息内容荣 | 参数内容为”all“时表示查询所有内容 |

* 参数值

| 值              | 说明                  |
| --------------- | --------------------- |
| my_id           | id                    |
| my_name         | 姓名                  |
| my_phone        | 电话                  |
| my_sex          | 性别                  |
| my_email        | 邮箱                  |
| my_birthday     | 生日 格式：2022.02.22 |
| my_qq           | qq号                  |
| my_address      | 地址                  |
| my_koseki       | 户籍                  |
| my_education    | 学历                  |
| my_school       | 学校                  |
| my_professional | 专业                  |
| my_state        | 状态                  |
| my_signature    | 签名 （段落）         |
| my_hobbyies     | 爱好 （段落）         |

* 响应参数：和上面参数值相同

* 响应数据：

```json
{
    "my_id": 1,
    "my_name": "陶继鑫",
    "my_phone": "18581766104",
    "my_sex": "男",
    "my_email": "491675919@qq.com",
    "my_birthday": "2001.07.24",
    "my_qq": "491675919",
    "my_address": "四川省资阳市",
    "my_koseki": "四川省资阳市",
    "my_education": "本科",
    "my_school": "四川工商学院",
    "my_professional": "软件工程",
    "my_state": "学生就读",
    "my_signature": "如果debugging是一种消灭bug的过程，那编程就一定是把bug放进去的过程。",
    "my_hobbyies": "吃饭睡觉打豆豆！"
}
```

### 2.修改个人信息接口

* 请求路径：/updateintroduce
* 请求方式：post
* 请求参数

| 参数名     | 参数说明       | 备注                                   |
| ---------- | -------------- | -------------------------------------- |
| queryKey   | 需要修改的信息 | 值和获**取个人信息接口**中的参数值相同 |
| updateData | 修改的内容     |                                        |

* 响应参数

* 响应数据

```javascript
"修改成功！"
```

### 3.修改个人全部信息

* 请求路径：/updateallintro
* post
* 请求参数

| 参数名       | 参数说明               | 备注         |
| ------------ | ---------------------- | ------------ |
| personalForm | 包含个人全部信息的对象 | 包含以下数据 |

```
{
    "my_id": 1,
    "my_name": "陶继鑫",
    "my_phone": "18581766104",
    "my_sex": "男",
    "my_email": "491675919@qq.com",
    "my_birthday": "2001.07.24",
    "my_qq": "491675919",
    "my_address": "四川省资阳市",
    "my_koseki": "四川省资阳市",
    "my_education": "本科",
    "my_school": "四川工商学院",
    "my_professional": "软件工程",
    "my_state": "学生就读",
    "my_signature": "如果debugging是一种消灭bug的过程，那编程就一定是把bug放进去的过程。",
    "my_hobbyies": "吃饭睡觉打豆豆！"
}
```

* 响应参数
* 响应数据

```
"修改成功"
"修改失败"
```



## 五、留言

### 1.获取留言

> 根据页数与行数获取留言。

* 请求路径：/getsomecomments
* 请求方式：post
* 请求参数：

| 参数名 | 参数说明 | 备注 |
| ------ | -------- | ---- |
| page   | 第几页   |      |
| num    | 一页几个 |      |

* 响应参数：

| 参数名      | 参数说明 | 备注 |
| ----------- | -------- | ---- |
| id          |          |      |
| com_name    | 昵称     |      |
| create_time | 日期     |      |
| good_number | 点赞数   |      |
| com_content | 评论内容 |      |

* 响应数据：

```javascript
[
    {
        "id": 15,
        "com_name": "",
        "create_time": "2022-04-19T23:56:52.000Z",
        "good_number": 0,
        "com_content": ""
    },
    ······
    {
        "id": 24,
        "com_name": "地方撒",
        "create_time": "2022-04-20T00:15:14.000Z",
        "good_number": 0,
        "com_content": "算法"
    }
]
```

### 2.获取留言总数

* 请求路径：/getcommenttotal
* 请求方式：post
* 请求参数：无
* 响应参数：返回的是一个数组，包含一个对象，对象中有参数

| 参数名 | 参数说明 | 备注 |
| ------ | -------- | ---- |
| total  | 评论总数 |      |

* 响应数据

```json
[
    {
        "total": 70
    }
]
```

### 3.删除某条评论

> 根据id删除某条评论。

* 请求路径： /delsomecomment
* 请求方式：delete
* 请求参数：

| 参数名 | 参数说明         | 备注 |
| ------ | ---------------- | ---- |
| delId  | 要删除的评论的id |      |

* 响应参数
* 响应数据

```json
"删除成功！"
```



## 六、图片

### 1.上传图片接口

> 上传图片，第一次上传为正常上传，第二次上传为更新图片及图片信息。

* 请求路径：/demoimg
* 请求方式：post
* 请求参数：

| 参数名  | 参数说明 | 备注 |
| ------- | -------- | ---- |
| demo_id | demo的id |      |

* 响应参数
* 响应数据：

```json
{
    "state": 200,
    "message": "更新成功！"
}
```

### 2.获取图片接口

* 请求路径：/getdemoimg?demo_id=？
* 请求方式：post
* 请求参数：post请求路径携带参数为demo的id
* 响应参数
* 响应数据：直接为图片













