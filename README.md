# Micro Service

## 如何权衡微服务的利弊？
### 利：
- 强模块化边界
  - 模块化：类 -》 类库 -》 服务模块化
- 可独立部署
  - 不需要团队合作来部署
- 技术多样性
  - 不同的技术团队可以根据自己的技术栈来开发服务

### 弊：
- 分布式复杂性
  - 多个服务，比起一个团队开发的项目，系统会更复杂
  - 一般的团队没办法理解整个系统的运作的
- 最终一致性
  - 数据一致性，比如不同的服务有不同的数据拷贝，数据在某个地方修改了，没有在另外一个地方修改，可能会导致问题
- 运维复杂性
  - 运维需要监控很多个不同的系统
- 测试复杂性
  - 需要测试多个不同的服务，可能需要不同的团队来一起测试

## 康威法则和微服务给架构师怎样的启示？
康威的原文中提出的各定律：
- 第一定律 組織溝通方式會通過系統設計表達出來
- 第二定律 時間再多一件事情也不可能做的完美，但總有時間做完一件事情
- 第三定律 線型系統和線型組織架構間有潛在的異質同態特性
- 第四定律 大的系統組織總是比小系統更傾向於分解

单个团队 - 单个项目 - OK

多个团队 - 单个项目 - 不 OK，沟通成本很高，一个团队迭代新功能需要协同多个团队

多个团队 - 多个服务 - OK，沟通成本降低，方便团队协作，每个团队只需要维护自己的服务，研发效率更高效

## 企业应该在什么时候开始考虑引入微服务？

### 单个项目架构
- 复杂性上升
- 生产力下降

### 微服务架构
- 复杂性上升
- 生产力维持稳定

### 什么时候开始考虑微服务
- 单块优先，一开始的时候做单块，因为单块服务比较快，在验证一个商业模式是否有效地时候，尽快显开发出来，选择单块
- 如果一开始的时候就选择微服务，那么很多的时候把工作的重心放在了微服务的架构上了，而不是商业模式的开发
- 当团队规模变大的时候，考虑将单块项目改成微服务
- 可以逐步把有些模块拆分来做成微服务，逐步的成为完全的微服务

## 微服务的组织架构

### 传统企业的组织团队
- 产品管理专家团队
- 用户体验专家团队
- 研发专家团队
- 测试团队
- 。。。
- DBA团队
- 运维团队

当一个项目来的时候，会从各种团队中抽调人，来组成团队研发产品，当产品结束后，会回归到各自的团队中去。

传统项目的劣势：
- 沟通成本，比如产品和研发有很多沟通，研发和测试、运维等也有很多沟通，测试的反馈也很慢 -- 导致研发效率低下

### 微服务的企业组织团队

端到端的服务，每个微服务团队都要负责所有的部分，一个微服务团队要求形成闭环，每一个微服务团队都要负责从头到尾的部分
- Architect
- Design
- Develop
- Review
- Test
- Deploy
- Run
- Support

## 微服务的分层

### 基础服务
- 向上提供公共服务
- 原子性的通用的服务

### 聚合服务
- 对于不同的接入端，要有不同的适配

举个例子，有个电商网站，要给不同的设备介入端提供不同大小的商品（手机，电脑等）
- 基础服务：提供商品列表
- 聚合服务：call 基础服务，但会额外处理

## 微服务的重要基础设施 - 网关 API Gateway

- 在微服务中，有许多的 API 微服务，比如订单、购物车等，在架构中，通过调用这些 API 服务，可以实现一些功能
- 但是我们不希望外部的用户可以来调用他们，这就是 **Gateway** 网关的职责
- 对外只有一个统一的接口

层次（从外到内）
- User Interface
- Load Balance
- API Gateway
- Micro Service

Gateway 的功能
- 反向路由 ： 将外部的请求，转换成内部的请求调用
- 认证安全 ： “门卫”，对于恶意的行为进行抵制，比如爬虫和黑客等，要对这些请求行为进行认证
- 限流熔断 ： 如果有大量的容量突然进来了，内部的服务如果没有很好的处理的话，很可能会导致内部的瘫痪
- 日志监控 ： 将所有的访问情况作为日志存储下来

## Netflix 开源网关  Zuul
<img src='./zuul.png'>
https://github.com/Netflix/zuul

