gitBash连接远程服务器：ssh root@120.79.177.24





查找MySQL: dnf search mysql-server 

查看MySQL，这⾥的版本是8.0.21 : dnf info mysql-server 

安装MySQL，这⾥加-y的意思是依赖的内容也安装 : dnf install mysql-server -y

查看mysql是否启动成功：systemctl status mysqld

启动mysql：service mysqld start

让mysql跟随系统一起启动：systemctl enable mysqld

连接mysql数据库：mysql -u root -p

