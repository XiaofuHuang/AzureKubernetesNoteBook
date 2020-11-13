# Kubernetes API 服务器的安全防护

> 我们可以为API服务器配置一个或多个身份验证插件/授权插件


![authenticating_the_client_with_authentication_plugins](.\Images\12\authenticating_the_client_with_authentication_plugins.jpg)

## 概念

- User: 连接到API Server的客户端, 包括Human和Pod
- Service Account: 一种Kubernetes资源, 用来管理身份和权限
- Group: 用于一次将权限授予多个用户, 身份验证插件将返回组以及用户名和用户ID
   - system:unauthenticated
   - system:authenticated
   - system:serviceaccounts
   - system:serviceaccounts:\<namespace\>

## Service Account
API服务器要求客户端在允许其对服务器执行操作之前对其进行身份验证.

### Pod如何进行身份验证
每个Pod与一个Service-Account关联,该Service-Account表示在Pod中运行的应用程序的身份.Token文件包含ServiceAccount的身份验证token.当应用程序使用此token连接到API服务器时,身份验证插件将对ServiceAccount进行身份验证,并将ServiceAccount的用户名传递回API server core.



