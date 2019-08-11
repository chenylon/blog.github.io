## AWS api-gateway 管理VPC私有HTTP/HTTPS API
AWS API gateway 提供了一整套部署和管理API的方法。通过VPC link，api gateway可以访问VPC内的private resource。

### 项目需求
通过api gateway 将VPC内private subnet的api接口中的一部分对外开放，并通过IP限制请求。

### AWS 组件
- API gateway
- NLB
- WAF

### 整体架构
![](images/api-gateway/架构图.png)

### EC2测试机
在VPC的private subnet内创建一台nginx server，并设置一个location：
```nginx
location /ping {
    default_type application/json;
    return 200 '{"hello" : "world"}';
}
```

### 配置NLB(internal)
由于VPC内的资源不对外开放，api gateway无法从public internet获取VPC内资源，所以必须通过VPC Link获取。VPC Link需要从NLB（不支持ALB）建立api gateway到VPC的链接。
参考：<https://docs.aws.amazon.com/apigateway/latest/developerguide/set-up-private-integration.html>
创建一个NLB名为: test-for-NLB, 监听80端口，target group中的backend为刚才创建的EC2测试机。

### 配置VPC Link
在API gateway控制台的左侧导航栏中选择VPC Links->Create。在Target NLB中选择刚才创建的test-for-NLB。

### 配置API gateway
在API gateway控制台的左侧导航栏中选择APIs -> Create API
![](images/api-gateway/create_api.png)

