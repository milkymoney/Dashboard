# 架构设计
我们的程序采用Client-Server(CS)架构。前端（Client）采用微信小程序与用户交互，后端（Server）使用Golang搭建服务器，使用MySQL作为数据库存储用户数据。

程序的前端后端都使用MVC架构。MVC架构将应用程序划分为三种组件：模型，视图，控制器。

- 模型（Model） 用于封装与应用程序的业务逻辑相关的数据以及对数据的处理方法。Model有对数据直接访问的权力，例如对数据库的访问。Model不依赖View和Controller，也就是说， Model不关心它会被如何显示或是如何被操作。但是Model中数据的变化一般会通过一种刷新机制被公布。
- 视图（View）能够实现数据有目的的显示。在 View 中一般没有程序上的逻辑。为了实现 View 上的刷新功能，View 需要访问它监视的数据模型（Model），因此应该事先在被它监视的数据那里注册。
- 控制器（Controller）起到不同层面间的组织作用，用于控制应用程序的流程。它处理事件并作出响应。“事件”包括用户的行为和数据 Model 上的改变。

## 前端
前端我们采用微信小程序进行开发。微信小程序的架构学习自前端的Vue框架，有着和Vue同样的结构风格。前端的文件对于MVC的划分比较明晰。
### Model
用来存储数据的地方，具体为(./pages)里面的所有js文件里面的(page({}))里面的data对象里面的变量，这些数据与视图和控制器的逻辑相对独立开来。(./app.json,./project.config.json)的配置信息也属于Model的范畴。
### View
前端的页面展示为每个(./pages)下面的所有wxml和wxss文件，除此之外，(./dict)下面的所有文件都是提供UI支持的。
### Controller
控制器用来对数据的输入输出和展示进行处理，具体为(./pages)里面的所有js文件里面的(page({}))里面除了data之外的函数，这些都是用于对前端的业务进行处理的函数。除此之外，还有(./app.js)的处理全局函数。

## 后端
### Model
在后端，Model控制着任务（./models/task.go），用户（./models/user.go）以及他们的关系（./models/relationship.go）。Model承担管理数据的职能，负责与数据库交互的工作。
### View
后端没有图形显示界面，对外显示的功能体现为对前端请求的响应。当前端请求到来时，beego框架（main.go）会调用路由模块（./routers/router.go），路由模块调用（Controller）提供的接口，获取数据，并在处理后返回合适的结果给用户。
### Controller
Controller（./controllers）管理Model的内容，给View模块提供合适的数据。

# 界面设计
## 接受任务
### 首页
![设计图](https://github.com/milkymoney/Dashboard/blob/master/pic/UI%E8%8D%89%E5%9B%BE_%E4%BB%BB%E5%8A%A1%E6%8E%A5%E5%8F%97/%E6%8E%A5%E5%8F%97%E4%BB%BB%E5%8A%A1-1-%E9%A6%96%E9%A1%B5.png)
### 找任务
![设计图](https://github.com/milkymoney/Dashboard/blob/master/pic/UI%E8%8D%89%E5%9B%BE_%E4%BB%BB%E5%8A%A1%E6%8E%A5%E5%8F%97/%E6%8E%A5%E5%8F%97%E4%BB%BB%E5%8A%A1-2-%E6%89%BE%E4%BB%BB%E5%8A%A1.png)
### 任务详情
![设计图](https://github.com/milkymoney/Dashboard/blob/master/pic/UI%E8%8D%89%E5%9B%BE_%E4%BB%BB%E5%8A%A1%E6%8E%A5%E5%8F%97/%E6%8E%A5%E5%8F%97%E4%BB%BB%E5%8A%A1-3-%E4%BB%BB%E5%8A%A1%E8%AF%A6%E6%83%85.png)
### 任务审核
![设计图](https://github.com/milkymoney/Dashboard/blob/master/pic/UI%E8%8D%89%E5%9B%BE_%E4%BB%BB%E5%8A%A1%E6%8E%A5%E5%8F%97/%E6%8E%A5%E5%8F%97%E4%BB%BB%E5%8A%A1-4-%E4%BB%BB%E5%8A%A1%E5%AE%A1%E6%A0%B8.png)
### 任务中：问卷
![设计图](https://github.com/milkymoney/Dashboard/blob/master/pic/UI%E8%8D%89%E5%9B%BE_%E4%BB%BB%E5%8A%A1%E6%8E%A5%E5%8F%97/%E6%8E%A5%E5%8F%97%E4%BB%BB%E5%8A%A1-5-%E4%BB%BB%E5%8A%A1%E4%B8%AD%EF%BC%9A%E9%97%AE%E5%8D%B7.png)
### 任务袋
![设计图](https://github.com/milkymoney/Dashboard/blob/master/pic/UI%E8%8D%89%E5%9B%BE_%E4%BB%BB%E5%8A%A1%E6%8E%A5%E5%8F%97/%E6%8E%A5%E5%8F%97%E4%BB%BB%E5%8A%A1-6-%E4%BB%BB%E5%8A%A1%E8%A2%8B.png)

# 功能模型
功能模型文档见[github文档](https://github.com/milkymoney/Dashboard/blob/master/system.md)。

# 领域模型
在设计中，我们有user和task两种对象。user和task之间的关系有用户发布任务（release），用户接受任务（accept）两种关系。用户接受任务后，需要上传确认图片作为证明（ConfirmImage）
![domain](https://github.com/milkymoney/Dashboard/blob/master/domain.png?raw=true)

# 数据库设计
数据库的ER图如下：  
![ER图](https://github.com/milkymoney/Dashboard/blob/master/ER%E5%9B%BE.png?raw=true)

# API设计
接口文档见[github文档](https://github.com/milkymoney/Dashboard/blob/master/api.yaml)，推荐复制到[swagger编辑器](https://editor.swagger.io/)上查看。

# 用例设计
用例设计见[github文档](https://github.com/milkymoney/Dashboard/blob/master/usecase.md)。
