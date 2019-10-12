# 分布式任务调度平台XXL-JOB搭建教程
## 一、源码下载地址
### www.baidu.com
## 二、源码结构
##### xxl-job-admin：调度中心，作用：统一管理任务调度平台上调度任务，负责触发调度执行，并且提供任务管理平台。
##### xxl-job-core：公共依赖
##### xxl-job-executor-samples：xxl-job-executor-sample-springboot 执行器，作用：负责接收“调度中心”的调度并执行；可直接部署执行器，也可以将执行器集成到现有业务项目中。
tupian.jpg
## 三、快速开始
## 3.1 先配置xxl-job-admin：调度中心工程

### 3.1.0 初始化“调度数据库”
##### "调度数据库初始化SQL脚本" 位置为:
##### /xxl-job/doc/db/tables_xxl_job.sql

### 3.1.1 修改调度中心配置
##### 文件位置为:
##### /xxl-job/xxl-job-admin/src/main/resources/application.properties
##### **主要修改jdbc连接，若需报警邮箱功能也可以配置**
##### JDBC链接：
##### spring.datasource.url=jdbc:mysql://127.0.0.1:3306/xxl_job?Unicode=true&characterEncoding=UTF-8
##### spring.datasource.username=root
##### spring.datasource.password=root_pwd
##### spring.datasource.driver-class-name=com.mysql.jdbc.Driver
##### 报警邮箱
##### spring.mail.host=smtp.qq.com
##### spring.mail.port=25
##### spring.mail.username=xxx@qq.com
##### spring.mail.password=xxx
##### spring.mail.properties.mail.smtp.auth=true
##### spring.mail.properties.mail.smtp.starttls.enable=true
##### spring.mail.properties.mail.smtp.starttls.required=true
##### spring.mail.properties.mail.smtp.socketFactory.class=javax.net.ssl.SSLSocketFactory

### 3.1.2 启动调度中心项目
##### 如果已经正确进行上述配置，直接运行/xxl-job/xxl-job-admin/src/main/com.xxl.job.admin/XxlJobAdminApplication.class
##### 调度中心访问地址：http://localhost:8080/xxl-job-admin，默认账号：admin，默认密码：123456
### 至此“调度中心”项目已经部署成功。

## 3.2 配置xxl-job-executor-sample-springboot：执行器工程
### 3.2.1
##### 确认pom文件中引入了 "xxl-job-core" 的maven依赖；

### 3.2.2 修改执行器工程配置
##### 文件位置为:
##### /xxl-job/xxl-job-executor-samples/xxl-job-executor-sample-springboot/src/main/resources/application.properties

##### 执行器配置
##### **主要修改xxl.job.admin.addresses地址，配置调度中心地址**
##### 调度中心部署跟地址 [选填]：如调度中心集群部署存在多个地址则用逗号分隔。执行器将会使用该地址进行"执行器心跳注册"和"任务结果回调"；为空则关闭自动注册；
##### xxl.job.admin.addresses=http://127.0.0.1:8080/xxl-job-admin
##### 执行器AppName [选填]：执行器心跳注册分组依据；为空则关闭自动注册
##### xxl.job.executor.appname=xxl-job-executor-sample
##### 执行器IP [选填]：默认为空表示自动获取IP，多网卡时可手动设置指定IP，该IP不会绑定Host仅作为通讯实用；地址信息用于 "执行器注册" 和 "调度中心请求并触发任务"；
##### xxl.job.executor.ip=
##### 执行器端口号 [选填]：小于等于0则自动获取；默认端口为9999，单机部署多个执行器时，注意要配置不同执行器端口；
##### xxl.job.executor.port=9999
##### 执行器通讯TOKEN [选填]：非空时启用；
##### xxl.job.accessToken=
##### 执行器运行日志文件存储磁盘路径 [选填] ：需要对该路径拥有读写权限；为空则使用默认路径；
##### xxl.job.executor.logpath=/data/applogs/xxl-job/jobhandler
##### 执行器日志保存天数 [选填] ：值大于3时生效，启用执行器Log文件定期清理功能，否则不生效；
##### xxl.job.executor.logretentiondays=-1

### 3.2.3 启动调度中心项目
##### 如果已经正确进行上述配置，直接运行/xxl-job/xxl-job-executor-samples/xxl-job-executor-sample-springboot/src/main/com.xxl.job.executor/XxlJobExecutorApplication.class
### 至此“执行器”项目已经部署成功。

## 3.3 开发定时任务
### 步骤1：
登录调度中心，点击下图所示“新建任务”按钮，新建示例任务。然后，参考下面截图中任务的参数配置，点击保存
![RUNOOB 图标](https://github.com/haohonghh/xxl-job/blob/master/QQ%E5%9B%BE%E7%89%8720190926102816.png "RUNOOB")






