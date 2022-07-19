### 请严格按照教程操作；不要自己改库名、改包名、改服务端口，教程上没有说的就不要动，这样出了问题我们才好给你排查，等你熟悉项目了再改也不迟；因自己改了教程之外的东西出了问题来咨询技术的，我们都不受理

### 开发环境准备（注意版本）

- windows系统（确保你的开发电脑内存充足，16G起步）
- IntelliJ IDEA（**一定要安装lombok插件**） + WebStorm + HBuilder X + [微信开发者工具](https://developers.weixin.qq.com/miniprogram/dev/devtools/download.html)
- MySql8（MySql版本至少5.7或者5.7+，强烈推荐mysql8，建议安装在本机或同一局域网，否则可能会因为网络问题引起超时）
- Redis（建议安装在本机或同一局域网，否则可能会因为网络问题引起超时）
- JDK8
- maven v3.6.0（后端项目构建管理）
- node v14.0.0（前端构建管理）
- npm v6.14.4
- SwitchHosts（用于修改hosts）
- 阿里OSS、七牛云、minio、腾讯cos 四选一
- 阿里短信
- 申请好小程序一个（我们演示小程序的类目是：商家自营 > 家电/数码/手机）
- 申请好微信支付服务商一个
- 申请极光IM应用一个
- 必须保证机器的外部网络是通的

### 了解项目结构

- [https://git.joolun.com/joolun-multi/joolun-plus/wiki/A-%E9%A1%B9%E7%9B%AE%E7%BB%93%E6%9E%84%E8%AF%B4%E6%98%8E](https://git.joolun.com/joolun-multi/joolun-plus/wiki/A-项目结构说明)

### 下载源码(https://git.joolun.com/joolun-multi/joolun-plus)

- [![img](https://joolun-blog.oss-cn-zhangjiakou.aliyuncs.com/git/QQ%E6%88%AA%E5%9B%BE20200613090615.png)](https://joolun-blog.oss-cn-zhangjiakou.aliyuncs.com/git/QQ截图20200613090615.png)

### 项目导入

- 直接从git私服页面上下载源码，分别将joolun-plus项目导入到idea，joolun-plus-ui项目导入到webstorm，joolun-plus-uniapp、joolun-plus-app项目导入到HBuilder X

### 修改hosts

- 以管理员的身份运行SwitchHosts!，添加如下配置（假如你的mysql没在本机，把127.0.0.1换成实际ip就行了）

- hosts修改方法有多种，推荐使用SwitchHosts!工具，其他方法请自行百度

- **❗特别说明：请一定要按此步骤配置hosts，禁止修改代码中配置成IP或localhost**

- hosts配置完成后，逐个ping joolun-xx 确认可以使用!

  ```text
  # 本地开发环境 
  127.0.0.1 joolun-nacos 
  127.0.0.1 joolun-gateway 
  127.0.0.1 joolun-redis 
  127.0.0.1 joolun-mysql
  ```

  [![img](https://joolun-blog.oss-cn-zhangjiakou.aliyuncs.com/git/20191128112734_n8usaf74n1%5B1%5D.png)](https://joolun-blog.oss-cn-zhangjiakou.aliyuncs.com/git/20191128112734_n8usaf74n1[1].png)

- 再用数据库工具直接连joolun-mysql，看能否连接上MySQL，确保hosts成功修改

  [![img](https://joolun-blog.oss-cn-zhangjiakou.aliyuncs.com/git/QQ%E6%88%AA%E5%9B%BE20200804105820.jpg)](https://joolun-blog.oss-cn-zhangjiakou.aliyuncs.com/git/QQ截图20200804105820.jpg)

### 导入数据库（joolun-plus/db）再次重申mysql版本必须在5.7或以上，最好是mysql8，不然系统无法运行

- 依次将db目录下的.sql脚本导入到mysql（4个库都要导入），【升级脚本】不用管，版本升级时才有用
- 注意：mysql5.7脚本导入报“Unknown collation: 'utf8mb4_0900_ai_ci'“错，请把脚本中的所有”utf8mb4_0900_ai_ci”换成“utf8mb4_bin”，当然你也可以把mysql版本升到8.0.1以上，毕竟8的在性能方面提升很大

### 后端服务（joolun-plus）发布

- idea打开（file-open）后端代码（joolun-plus）-->配置maven-->等待maven下载完相应的jar包-->再安装lombok插件

  [![img](https://joolun-blog.oss-cn-zhangjiakou.aliyuncs.com/git/QQ%E6%88%AA%E5%9B%BE20200330124903.png)](https://joolun-blog.oss-cn-zhangjiakou.aliyuncs.com/git/QQ截图20200330124903.png) [![img](https://joolun-blog.oss-cn-zhangjiakou.aliyuncs.com/git/20210409141652.png)](https://joolun-blog.oss-cn-zhangjiakou.aliyuncs.com/git/20210409141652.png)

- 修改nacos配置文件中的数据库账号密码（joolun-plus/server/nacos-server/conf/application.properties） [![img](https://joolun-blog.oss-cn-zhangjiakou.aliyuncs.com/git/20200907172303.jpg)](https://joolun-blog.oss-cn-zhangjiakou.aliyuncs.com/git/20200907172303.jpg)

- 双击（joolun-plus/server/nacos-server/bin/startup.cmd）启动nacos，nacos要一直运行不要关了（Mac或其他系统请查看[nacos官网](https://nacos.io/zh-cn/docs/deployment.html)，要单机模式启动）；nacos包我们直接在官方下载的，没有做任何二开，如启动不了肯定就是你系统环境问题，请自行解决

  [![img](https://joolun-blog.oss-cn-zhangjiakou.aliyuncs.com/git/QQ%E6%88%AA%E5%9B%BE20200211113553.png)](https://joolun-blog.oss-cn-zhangjiakou.aliyuncs.com/git/QQ截图20200211113553.png)

- nacos启动成功后，浏览器中打开http://joolun-nacos:8848/nacos/index.html 账号密码：nacos/nacos

- nacos中修改相关密码 [![img](https://joolun-blog.oss-cn-zhangjiakou.aliyuncs.com/git/QQ%E6%88%AA%E5%9B%BE20200804142629.jpg)](https://joolun-blog.oss-cn-zhangjiakou.aliyuncs.com/git/QQ截图20200804142629.jpg) application-dev.yml：修改redis密码，配置极光IM信息

  joolun-auth-dev.yml、joolun-codegen-dev.yml、joolun-upms-admin-dev.yml、joolun-weixin-admin-dev.yml、joolun-mall-admin-dev.yml、joolun-mall-api-dev.yml：修改mysql账号、密码，将root换成自己的账号密码

  注意冒号后面要带一个空格，redis和mysql的密码不要用纯数字，否则无法启动

  [![img](https://joolun-blog.oss-cn-zhangjiakou.aliyuncs.com/git/20191128112734_x2swv87.png)](https://joolun-blog.oss-cn-zhangjiakou.aliyuncs.com/git/20191128112734_x2swv87.png)

- 然后idea依次启动

  ```text
  JooLunGateWayApplication（网关） 
  JooLunAuthApplication（认证授权） 
  JooLunUpmsApplication（后台管理模块） 
  JooLunWeiXinApplication（微信管理模块） 
  JooLunCodeGenApplication（代码生成模块） 
  JooLunMallApplication（商城管理模块）
  JooLunMallApiApplication（商城API模块）
  JooLunPayApiApplication（商城支付模块）
  ```

  注意每个服务是否有报错

  [![img](https://joolun-blog.oss-cn-zhangjiakou.aliyuncs.com/git/QQ%E6%88%AA%E5%9B%BE20200729123529.jpg)](https://joolun-blog.oss-cn-zhangjiakou.aliyuncs.com/git/QQ截图20200729123529.jpg)

- 将redis的key过期推送功能打开，否则订单无法自动取消（自行百度redis的key过期推送怎么打开）

- 后台【文件存储配置】配置存储服务，不配无法上传图片，详情查看文档[【文件存储功能】](https://git.joolun.com/joolun-multi/joolun-plus/wiki/A-文件上传和存储功能)

### 后端页面（joolun-plus-ui）发布

- 特别说明：请不要自己随意升级package.json里的sdk版本，特别是avue版本，很可能会引起很多问题

- 确认已经安装好了node和npm

- WebStorm打开（file-open）前端代码（joolun-plus-ui）

- 在joolun-plus-ui目录下运用如下命令

  ```text
  npm install --registry=https://registry.npm.taobao.org
  ```

  [安装node-sass失败](https://git.joolun.com/joolun-multi/joolun-plus/issues/340) [![img](https://joolun-blog.oss-cn-zhangjiakou.aliyuncs.com/git/20191229173112_0a9j5uvy3s%5B1%5D.png)](https://joolun-blog.oss-cn-zhangjiakou.aliyuncs.com/git/20191229173112_0a9j5uvy3s[1].png)

- install完成后，再运用`npm run serve`，如下图

  [![img](https://joolun-blog.oss-cn-zhangjiakou.aliyuncs.com/git/20191128112734_sdt864ww6a.png)](https://joolun-blog.oss-cn-zhangjiakou.aliyuncs.com/git/20191128112734_sdt864ww6a.png)

  [![img](https://joolun-blog.oss-cn-zhangjiakou.aliyuncs.com/git/20191128112734_8ayqxr0la4.png)](https://joolun-blog.oss-cn-zhangjiakou.aliyuncs.com/git/20191128112734_8ayqxr0la4.png)

- 访问地址：localhost:8082 管理员账号密码：admin/123456

[![img](https://joolun-blog.oss-cn-zhangjiakou.aliyuncs.com/git/20201214130535.png)](https://joolun-blog.oss-cn-zhangjiakou.aliyuncs.com/git/20201214130535.png)

### 后台服务不在本机

- 在实际开放过程中，前后端可能会由不同的人开发，所以后台服务（joolun-plus）可能不在本地，而是运行在其他同事电脑上。所以需要改下接口访问地址
- 后端页面：修改`joolun-plus-ui/vue.config.js`中的url；直接是网关服务（默认：ip:9999）的访问地址
- 小程序端：修改`joolun-plus-uniapp/config/env.js`中的basePath；可以是后台（joolun-plus-ui）访问地址，也可以直接是网关服务（默认：ip:9999）的访问地址
- H5端：修改`joolun-plus-uniapp/manifest.json`中的转发代理地址；可以是后台（joolun-plus-ui）访问地址，也可以直接是网关服务（默认：ip:9999）的访问地址

[![img](https://joolun-blog.oss-cn-zhangjiakou.aliyuncs.com/git/QQ%E6%88%AA%E5%9B%BE20200805144940.jpg)](https://joolun-blog.oss-cn-zhangjiakou.aliyuncs.com/git/QQ截图20200805144940.jpg)