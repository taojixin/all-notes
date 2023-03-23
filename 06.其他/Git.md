## Git基本使用

### 一、git常用命令

#### 1.设置用户签名

> Git 首次安装必须设置一下用户签名，否则无法提交代码。
>
> 这里设置用户签名和将来登录 github（或其他代码托管中心）的账号没有任 何关系。

* **git config --global user.name 用户名** 
* **git config --global user.email 邮箱**

#### 2.初始化本地库

* **git init**

#### 3.查看本地库状态

* **git status**

#### 4.添加暂存区

* **git add 文件名**

#### 5.提交本地库

* **git commit -m "日志信息" 文件名**

#### 6.查看历史版本

* **git reflog**
* **git log**

#### 7.版本穿梭

**git reset --hard 版本号**



### 二、分支操作

#### 1.查看分支

* **git branch -v**

##### 2.创建分支

* **git branch 分支名**

#### 3.切换分支

* **git checkout 分支名**

#### 4.合并分支

* **git merge 分支名**   

注：可能产生冲突



### 三、远程仓库操作

#### 1.查看当前所有远程库地址别名

* **git remote -v**

#### 2.创建远程仓库别名

* **git remote add 别名 远程地址**

`git remote add ori https://github.com/atguiguyueyue/git-shTest.git`

#### 3.推送本地分支到远程仓库

* **git push 别名 分支**

#### 4.克隆远程仓库到本地

* **git clone 远程地址**

#### 5.拉取远程仓库代码

> 注意拉去和克隆的不同

* git pull 远程地址 master