# v2ray-web-manager 
 [![Build Status](https://travis-ci.com/master-coder-ll/v2ray-web-manager.svg?branch=master)](https://travis-ci.com/master-coder-ll/v2ray-web-manager) 

 v2ray-web-manager 项目包含admin管理端和proxy端，admin端提供管理功能。proxy端提供核心的流量控制、账号识别、流量转发功能，
 同时支持多种转发流量模型（1对1，1对多）。
 
 项目核心是工作在传输层的中间件，位于用户与v2ray链路之间。通过转发流量实现。理论上支持上层所有的协议，现适配了ws协议。 
 
 ssl/tls 支持使用nginx 等工具提供，也可以套cdn提供。
 
  ## 特征：
  * 流量控制(qos)-无敌的速率、流量、连接数控制 ，一切都可以灵活定制
  * 账号管理
  * 流量管理-到期自动、流量超标断开连接
  * 服务器管理 
  * 公告管理
  * 分权限
  * 邀请码注册
  * 订阅
  * 等级
 
 
 
#### 如果能帮助到你，请`watch` `star` `Fork`
  
 ## 前端项目
   [前端项目->v2ray-manager-console](https://github.com/master-coder-ll/v2ray-manager-console)
 

 
 ## 简要视图
 服务器配置
 ![服务器](https://github.com/master-coder-ll/v2ray-web-manager/raw/master/static/admin_index.png)
 
 管理员帐号页面 
 ![管理员账号](https://github.com/master-coder-ll/v2ray-web-manager/raw/master/static/admin_account.png)
 
普通用户看到页面
 ![管理员账号]( https://raw.githubusercontent.com/master-coder-ll/v2ray-web-manager/master/static/my-account.png)

更多页面，请自己尝试。
 
 ## 1.开始使用 
   
 #### 系统要求
 
    * java8 以上
    * 内存大于等于300M
    * cpu vCPU 1核心
    * nginx 或者其他具有相同功能
    * java8 +


   
 #### 新手
 
  [一步一步跟着我从零安装](https://github.com/master-coder-ll/v2ray-web-manager/blob/master/step-by-step-install.md)
  
  [一步一步跟着我从零配置网站](https://github.com/master-coder-ll/v2ray-web-manager/blob/master/step-by-step-conf.md)
 

  #### 模式和配置
  
  [模式和配置](https://github.com/master-coder-ll/v2ray-web-manager/blob/master/step-by-step-model.md)

## 2.维护与治理 

### 数据库

   数据库-默认情况下会在 `/opt/jar/db` 生成admin.db 定时保存就好

### 更新/升级

  #### [更新日志](https://github.com/master-coder-ll/v2ray-web-manager/blob/master/updated-log.md)


### 旧版升级到V3.0+ 特别注意说明

#### 4.增强了ws接口的安全性。`原来的v2ray账号将失效`。

#### 5. 配置文件的更新，统一/和新增了参数 ,`旧版配置文件需要升级到新版`，要不通讯出错、程序不能运行。




+ 关闭java服务

```
    关闭 admin
    # ps -ef | grep admin-
    # kill [进程号]
    # ps -ef | grep v2ray-proxy-
    # kill [进程号]
 ```

+ 下载最新的release包

     [java服务-releases页面](https://github.com/master-coder-ll/v2ray-web-manager/releases)
         
     [前端服务-releases页面](https://github.com/master-coder-ll/v2ray-manager-console/releases)
        

+ 重新启动



     
### 优化
   #### 减少java 内存占用
   
   1. 使用其他jre 如：[openj9-eclipse](https://www.eclipse.org/openj9/),
   减低内存占用明显，并且不影响性能。

   2. `激进` ~~java:JIT特性是提高java性能的重要编译器，其动态编译优化性能更甚于c++等一些静态编译语言。但是也是内存占有用的大户。
               如果你需要减少内存占用，在运行java 命令上加 `-Djava.compiler=NONE` ，会大幅减少java内存占用(约30~50%)，同时降低性能,大幅度增加启动时间。
               出现一些动态代理的问题不要用。~~
        
     
  ## 参数说明
  ### 服务器配置参数
   1.  访问域名 如：test.com ,v2ray客户端显示的名称，可以是域名/IP
    
   2. 访问端口  https tls ->443 ,或者其他80 etc
   
   3. v2rayTag  当前v2ray config.json下默认`6001` 
    
  ### 账号参数
   1. 周期  结算周期 30 表示每30天，重置用户的流量统计
   
   2. 速率  1024KB/s ,单位KB/S
   
   3. 账号  组成v2ray path ，在当前配置下客户端会生成 path:/ws/账号/
   
   4. 流量 周期内可用流量数，单位GB
  
  ### 开启邀请码注册(release 大于 v2.0)
   管理员登录->参数列表->需要邀请码才能注册吗？默认 `false` ，开启 `true`  
   
       次要选项: 用户能邀请其他人注册吗？默认 false ，开启 true 
        
## 测试

### 限速测试
    
   说明: 本地带宽下行50Mpbs,上行约8Mpbs。admin端限速2MB/S, 测试结果如图：
    
![测试1](https://www.speedtest.net/result/8927382635.png)
   
   测试结果：下行16.36/8=2.1 刚刚好是admin端配置的2MB/S。
   
## 架构
现在架构：

![now](https://raw.githubusercontent.com/master-coder-ll/v2ray-web-manager/master/static/now.png)

未来架构(不继续开发)：

![架构1](https://raw.githubusercontent.com/master-coder-ll/v2ray-web-manager/master/static/future.png)

## 项目结构
   * common 公有
   * proxy 代理中间件-核心
        * 提供 账号解析支持
        * 提供 流量控制
        * 提供 流量上报
        * 提供 流量转发
   * v2ray-jdk v2ray rpc 支持包
   * vpn-admin 管理后台api 端
        * 提供 用户/账号等功能的管理
   
   
## 警告
请遵循你国家的法律下使用。仅供学习研究
## License
This project is licensed under the MIT License
