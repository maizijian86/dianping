# dianping

黑马点评（hmdp）项目的个人学习副本，用于本地运行与源码阅读。

## 来源说明

本仓库的 Java 源码、配置与 SQL 脚本复制自公开仓库
[KNeegcyao/dianping](https://github.com/KNeegcyao/dianping)（原作者未声明开源许可）。
原仓库的 README 未包含在本仓库中，本 README 为重新编写。
代码版权归原作者所有，这里仅作学习用途；如需商用请先联系原作者。

## 技术栈

- Spring Boot + MyBatis-Plus
- MySQL、Redis（Lettuce 连接池）、Redisson
- RabbitMQ
- Lua 脚本（秒杀库存扣减、分布式锁解锁）
- JWT 登录态 + 拦截器

## 目录结构

```
src/main/java/com/hmdp/
├── config/        # 各类配置（MVC、MyBatis、队列、Redisson）
├── controller/    # 接口层
├── service/       # 业务逻辑及实现
├── mapper/        # MyBatis-Plus Mapper
├── entity/ dto/   # 实体与传输对象
├── interceptor/   # 登录拦截器
├── listener/      # 消息监听
└── utils/         # 工具类（Redis、JWT、缓存等）

src/main/resources/
├── application.yaml   # 端口、数据源、Redis、RabbitMQ 配置
├── db/hmdp.sql        # 建库建表及初始数据
├── mapper/            # MyBatis XML
├── seckill.lua        # 秒杀脚本
└── unLock.lua         # 解锁脚本
```

## 本地运行

1. 准备环境：JDK 8+、Maven、MySQL、Redis，若用到秒杀下单需 RabbitMQ。
2. 导入建表脚本：

   ```bash
   mysql -u root -p < src/main/resources/db/hmdp.sql
   ```

3. 按自己的环境修改 `src/main/resources/application.yaml`：数据库地址、库名、账号密码，以及 Redis / RabbitMQ 连接信息。
   注意仓库中的库名是 `dingping`，密码是原作者本地密码，务必改成你自己的。
4. 启动：

   ```bash
   mvn spring-boot:run
   ```

   服务默认端口 `8081`。

前端静态页面不在本仓库中，需另外准备（原课程资料里由 nginx 提供）。

## 说明

- 本仓库不含源仓库的提交历史，是重新初始化后的一次性快照。
- 仅同步代码，未做任何功能修改。
