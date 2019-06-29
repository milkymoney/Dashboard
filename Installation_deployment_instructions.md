## 安装部署说明

### 安装的环境与步骤

服务器系统环境要求：linux64位系统，在CentOS7，Ubuntu18.04等版本下通过测试

服务器机器配置要求：在1G内存，单核CPU，50G硬盘的云环境下成功运行

部署命令：`make run`

外部服务需求：需求mysql服务器，要求创建支持utf-8编码的数据库demo，已经预先创建完成。

### 安装成功的测试方法

运行`curl localhost:8080/v1/task`可以拿到数据

### 常见问题的解决方法

1. 端口被占用，提示：`ListenAndServe:  listen tcp :8080: bind: address already in use`

使用`lsof -i:port`查找占用端口的应用，然后运行`kill pid`杀死应用。再次运行服务器即可。

2. 提示权限不够。

使用有足够权限的账户，或者使用`chmod`提权

3. 需要进行测试，需要在微信以外的环境创建用户。

运行测试版本客户端
