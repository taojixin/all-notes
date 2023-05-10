## nginx

* 重启nginx：**service nginx restart**



gitBash连接远程服务器：**ssh root@120.79.177.24**

## MySQL

* 查找MySQL: **dnf search mysql-server** 
* 查看MySQL，这⾥的版本是8.0.21 : **dnf info mysql-server** 
* 安装MySQL，这⾥加-y的意思是依赖的内容也安装 : **dnf install mysql-server -y**
* 查看mysql是否启动成功：**systemctl status mysqld**
* 启动mysql：**service mysqld start**
* 让mysql**跟随系统一起启动**：**systemctl enable mysqld**
* 连接mysql数据库：**mysql -u root -p**

### 1.mysql配置

* 设置密码：**mysql_secure_installation**
* 配置root使可以远程链接：
* * 1.使用mysql数据库：**use mysql**
  * 2.修改权限：**update user set host = '%' where user = 'root'**
  * 3.查看权限：**select host, user from user**
  * 4.配置生效：**FLUSH PRIVILEGES**





## 连接服务器

### 1.通过gitbash连接

* 连接命令：**SSH root@120.79.177.24**



## pm2

*  命名进程 **pm2 start app.js --name my-api** 
* 显示所有进程状态 **pm2 list**  
* 停⽌指定的进程 **pm2 stop 0**  
* 停⽌所有进程 **pm2 stop all**  
* 重启所有进程 **pm2 restart all**  
* 重启指定的进程 **pm2 restart 0**  
* 杀死指定的进程 **pm2 delete 0**  
* 杀死全部进程 **pm2 delete all**  
* 后台运⾏pm2，启动4个app.js，实现负载均衡 **pm2 start app.js -i 4**
