@TOC

> 在**express**中使用**mysql2**操作数据库时，进行**分页查询**时报错`Error Incorrect arguments to mysqld_stmt_execute`。

### 问题

**报错：**`Error: Incorrect arguments to mysqld_stmt_execute`

```javascript
// 根据条数和页数查询笔记
  async getSomeNote(num, page) {
    const fromNum = (page - 1) * num
    const statement = `SELECT id,note_title,note_describe,note_createtime,note_sort FROM notes_test LIMIT ?,?;`
    // 这里传入的参数fromNum，num有问题，此时他们是数字型
    const result = await connections.execute(statement, [fromNum, num])
    console.log(result[0]);
    return result[0]
  }
```



### 原因

> **statement**为操作数据库的查询语句，为**字符串**类型，execute的第二个参数中的内容会被插入到statement中，此时插入的数**number**类型，**应该插入字符串类型**，所以报错'**错误的参数**'。



### 解决

> 将传入的参数改为字符串类型即可。

```javascript
// 根据条数和页数查询笔记
  async getSomeNote(num, page) {
    const fromNum = (page - 1) * num
    const statement = `SELECT id,note_title,note_describe,note_createtime,note_sort FROM notes_test LIMIT ?,?;`
    // 直接进行字符串的拼接，将number类型转为字符型
    const result = await connections.execute(statement, [fromNum+'', num+''])
    console.log(result[0]);
    return result[0]
  }
```

