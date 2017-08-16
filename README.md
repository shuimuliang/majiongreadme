# 房卡棋牌游戏行业解决方案

----

## 开服务
### 开放源代码
* 账号系统
* 房间系统
* 公告系统
* 战绩回放

## 容器服务
* 一站式镜像
* 计算弹性扩缩容

## 运维服务
* GM管理后台
* 分销系统

----
##在容器上部署
![arch](http://oupthc6v2.bkt.clouddn.com/archorigin.jpg)

1.获取源代码
* 客户端 [https://github.com/shuimuliang/qnmahjongclient](https://github.com/shuimuliang/qnmahjongclient)
* 服务器 [https://github.com/shuimuliang/qnmahjongserver](https://github.com/shuimuliang/qnmahjongserver)
* GM管理后台
* 分销系统

2.部署镜像
#### mysql
- 安装 pocker pull mysql
- 启动 docker run --name first-mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123456 -d mysql
#### 麻将接入服，登陆服
- 编译 GOOS=linux GOARCH=amd64 go build -ldflags "-X main.branch=`git rev-parse --abbrev-ref HEAD` -X main.commit=`git rev-parse HEAD`"
- 配置 修改conf_pro.toml配置文件
- 安装 docker build -t qnmahjong . 
- 启动 login : docker run -it --rm --name qnmahjong_login --link first-mysql:mysql -p 5001:5001 qnmahjong login
- 启动 logic : docker run -it --rm --name qnmahjong_logic --link first-mysql:mysql -p 5002:5002 qnmahjong logic

3.编译客户端版本
* 客户端环境：游戏引擎为Cocos2dx-2.2.6，主要逻辑由Lua编写，场景UI用CocosBuilder生成
* 填写登陆服务器地址: IP:端口
-- 试用演示地址 http://100.100.33.99:5001

4.游戏运行截图
* 游戏登陆界面 ![游戏登陆页面](http://oupthc6v2.bkt.clouddn.com/login.jpg)
* 游戏大厅页面 ![游戏大厅页面](http://oupthc6v2.bkt.clouddn.com/room.jpg)
* 打牌效果图 ![游戏大厅页面](http://oupthc6v2.bkt.clouddn.com/desk.jpg)

---
