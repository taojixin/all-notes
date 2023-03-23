> 本地vue项目部署到服务器报错**405**，在本地vue项目访问远程接口正常，但是部署到服务器时却报错405，vue项目通过**poxy**代理跨域。

### 问题

> 本地vue项目部署到服务器报错405：
>
> `POST 405 （Method Note Allowed)`
>
> `Uncaught (in promise) Error: Request failed with status code 405`



### 原因

> 原来远程服务器中未在**nginx.conf**中配置**api**的请求地址。之前配置的是**pc端**页面的`api`，这次需要配置后台管理系统的`admin`，但是未配置所以出错。

![image-20220428181228931](\image\api与admin.png)



### 解决

![image-20220428181339865](.\image\api与admin2.png)

