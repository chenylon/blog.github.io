## AWS api-gateway 管理VPC私有HTTP/HTTPS API
AWS API gateway 提供了一整套部署和管理API的方法。通过VPC link，api gateway可以访问VPC内的private resource。
### 项目需求
通过api gateway 将VPC内private subnet的api接口中的一部分对外开放，并通过IP限制请求。

### AWS 组件
- API gateway
- NLB
- WAF

![avatar](https://drive.google.com/file/d/1Bt08OX9Csv9KTp-kc-C7O-8fTtNuJSA4/preview)
