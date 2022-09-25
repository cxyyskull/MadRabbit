# MadRabbit

> 获取授权文件后，改名为Rabbit.lic，放在Config目录下，容器启动命令已更新，需用新的启动命令

#### 目前功能：自动过点选、魔方和拼图验证以及对接打码平台过手势验证获取ck，wsck提交，比价领取优惠券，仅支持对接青龙、xdd、傻妞，不支持其他工具对接
#### 傻妞和青龙可共存，青龙配置为空时，无法使用网页端登录
#### 查询rabbit版本：http://你的rabbit地址/api/version
#### 更新rabbit：http://你的rabbit地址/api/update

# [👉科学上网的频道](https://t.me/Rabbit_one)

## 使用方法:
1、新建一个项目
```
sudo cd /root && mkdir-p Rabbit && cd Rabbit
```
2、创建一个目录放配置
```
cd /root/Rabbit && mkdir -p  Config
```
3、下载config.json 配置文件
单青龙下这个
```
cd /root/Rabbit/Config && wget -O Config.json  https://raw.githubusercontent.com/ht944/MadRabbit/main/oneConfig.json
```
国内用
```
cd /root/Rabbit/Config && wget -O Config.json  https://ghproxy.com/https://raw.githubusercontent.com/ht944/MadRabbit/main/oneConfig.json
```
多青龙对接的下这个
```
cd /root/Rabbit/Config && wget -O Config.json  https://raw.githubusercontent.com/ht944/MadRabbit/main/manyConfig.json
```
国内用
```
cd /root/Rabbit/Config && wget -O Config.json  https://ghproxy.com/https://raw.githubusercontent.com/ht944/MadRabbit/main/manyConfig.json
```
不配置青龙的下这个
```
cd /root/Rabbit/Config && wget -O Config.json  https://raw.githubusercontent.com/ht944/MadRabbit/main/noConfig.json
```
国内用
```
cd /root/Rabbit/Config && wget -O Config.json  https://ghproxy.com/https://raw.githubusercontent.com/ht944/MadRabbit/main/noConfig.json
```
4、修改配置文件，配置完后
```
cd /root/Rabbit
```

### 安装：(ARM架构的机器自己将latest改成arm)
#### 方案一：自行构建镜像(由于有人魔改Rabbit，不再开源)
先下载源码，上传到此文件夹，再运行接下来的命令
```

```
启动
```

```
#### 方案二：使用我的镜像
### 注意修改端口时，只能修改5701，不要修改1234。可以在其他目录创建项目，但是路径需要自己修改，小白建议直接默认
amd版本
```
docker pull ht944/rabbit:latest
```
切换到Rabbit目录
```
cd /root/Rabbit
```
启动
```
sudo docker run --name rabbit -p 5701:1234  -d  -v  /root/Rabbit/Config:/MadRabbit_amd/Config -it --privileged=true  --restart=always  ht944/rabbit:latest
```
arm版本
```
docker pull ht944/rabbit:arm
```
切换到Rabbit目录
```
cd /root/Rabbit
```
启动
```
sudo docker run --name rabbit -p 5701:1234  -d  -v  /root/Rabbit/Config:/MadRabbit_arm/Config -it --privileged=true  --restart=always  ht944/rabbit:arm
```

### 对接WXPUSHER
* 正常填写其他信息，回调接口填写：http://ip:port/api/bind


### 强调一遍
### 配置文件修改后，重新启动容器


## 版本升级（arm的需要改latest为arm）
1.停止容器
```
docker stop rabbit 
```
2.删除容器
```
docker rm rabbit
```
3.拉取新镜像（arm的需要改latest为arm）
```
docker pull ht944/rabbit:latest 
```
4.切换到
```
cd /root/Rabbit 
```
5.amd启动容器
```
sudo docker run --name rabbit -p 5701:1234  -d  -v  /root/Rabbit/Config:/MadRabbit_amd/Config -it --privileged=true  ht944/rabbit:latest
```
arm启动容器
```
sudo docker run --name rabbit -p 5701:1234  -d  -v  /root/Rabbit/Config:/MadRabbit_arm/Config -it --privileged=true  ht944/rabbit:arm
```

## amd一次执行上面所有命令
```
sudo docker stop rabbit && docker rm rabbit && docker pull ht944/rabbit:latest && cd /root/Rabbit && docker run --name rabbit -p 5701:1234  -d  -v  /root/Rabbit/Config:/MadRabbit_amd/Config -it --privileged=true  ht944/rabbit:latest
```
## ARM版本一次执行上面所有命令
```
sudo docker stop rabbit && docker rm rabbit && docker pull ht944/rabbit:arm && cd /root/Rabbit && docker run --name rabbit -p 5701:1234  -d  -v  /root/Rabbit/Config:/MadRabbit_arm/Config -it --privileged=true  ht944/rabbit:arm
```

### 对接xdd
1. rabbit的配置文件中自定义设置XDD_TOKEN的值，如：123456
2. rabbit的配置文件中设置你的XDD_URL的值，如：http://127.0.0.1:8080
3. rabbit的配置文件中Config参数设置为[]，如："Config": []
4. xdd中设置对应的apitoken
5. 设置完之后，重启rabbit和xdd

### 对接傻妞
1. rabbit的配置文件中自定义设置SILLY_TOKEN的值，如：123456
2. 傻妞可视化面板中设置ark2.0_token为刚刚设置的 SILLY_TOKEN,或者发送命令 set jd_cookie ark2.0_token xxx, xxx为刚刚的token值，例如：set jd_cookie ark2.0_token
3. 傻妞设置对接的rabbit地址，命令为: `set jd_cookie nolan_addr http://xxx:xxxx`，http://xxx:xxxx为你的rabbit地址，或者对接rabbit的快捷登录（需要rabbit的4.0.2版本以上）`set jd_cookie nolan_addr http://xxx:xxxx`
4. 设置完之后，重启rabbit和傻妞


### 👇更新日志👇

#### 4.0.3(amd/arm) 版本更新
* 删除比价，快捷登陆功能
* 适配星空，熊猫代理，将api设置在proxy立即可，注意提取api时设置数量为1
* 增加更新功能，输入http://ip:port/api/update可自动更新最新版
* 更改为默认使用打码方式
* 修复部分其他bug

#### 4.0.2(amd/arm) 版本更新
* 快捷登陆对接傻妞，需设置set jd_cookie nolan_addr http://ip:port/rabbit，需要更新最新版的傻妞
* xdd版本设置rabbit_url为http://ip:port/rabbit
* 修复部分其他bug

#### 4.0.1(amd/arm) 版本更新
* 修复接口登陆对接其他工具的问题
* 验证码类型可自行选择，目前特殊验证码的通过率极低，基本过不去，故开放图鉴打码方式，可通过配置图鉴账号密码，以及新的参数FORCE_CAPTCHA，设置为true为特殊验证码，false为手势验证码，同时手势验证码需要非腾讯阿里的ip，否则仍为特殊验证码
* 修复部分其他bug

#### 4.0.0 (amd/arm) 版本更新
* 新增接口方式登陆
* 适配最新的图形验证，但是通过率极低，手动测试50次通过1次
* 更换授权接口，大多数机器可访问授权

#### 3.2.2 (arm) 版本更新
* 更换授权接口，连接速度更快
* 增加网页资产查询，已登录账号可通过扫码方式进入个人中心

#### 3.2.1(amd/arm)版本更新
* 更换所有ip为非打码方式，采用自训练的模型
* 修复非打码方式报错问题

#### 3.2.0(amd/arm)版本更新
* 解决验证码识别问题，不依赖打码平台


#### 2.2.0(amd/arm)版本更新
* 为保障不被他人白嫖，强制更新最新版，老板本将无法使用
* 优化log计算方法，不再占用大内存，开启仅多占用10m内存
* 为防止log被他人爆破获取，5次失败会锁定，需重启
* 增加傻妞的token认证，对接傻妞需最新版rabbit，最新版傻妞，且傻妞配置 `set jd_cookie ark2.0_token xxxx`，rabbit须在最新配置文件中配置SILLY_TOKEN，二者需要保持一致

#### 2.1.6(amd/arm)版本更新
* 修复授权问题
* log请求需携带token，token需在配置文件中设置(请求示例：http://ip:port/api/log?token=123546)

#### 2.1.5(amd/arm)版本更新
* 修改授权，所有人必须更新最新版，无需重新获取授权
* 傻妞对接时，可以配置青龙，否则网页端无法使用
* 仅可对接青龙，xdd，芝士，不支持其他平台对接（芝士需更新最新版）
* 修复过期预警的时间戳判断问题
* 尝试修复网络问题

#### 2.1.4(amd/arm)版本更新
* 修复前端无法二验的问题
* 无授权机器可以启动rabbit，但是无法登陆
* 修复部分bug，主要为错误无提示，不回收问题
* 增加登陆时间，尝试解决网络差的机器无法获取验证码问题

#### 2.1.0(amd/arm)版本更新
* 不再需要腾讯阿里的ip，任何机器均可登陆
* 可以留空青龙配置，傻妞可对接rabbit
* 优化前端加载速度（感谢 @svips188 的优化）
* 更换授权域名
* 修复xdd不显示登陆成功的bug
* 修复log计算的bug
* 修复青龙配置有误无法进入主页的bug
* 修复一些影响正常使用的bug

#### 2.0.7(amd/arm)版本更新
* 适配青龙2.11及以上(需要青龙应用的系统权限)
* 修复大量bug，解决一些常见问题，如收不到验证码之类的

#### 2.0.6(amd/arm)版本更新
* 采取内置浏览器方式，无需下载浏览器
* 适配群辉机器
* 适配arm机器，arm机器拉取时更换后缀为arm

#### 2.0.5(amd)版本更新
* 修复xdd接口错误问题
* 浏览器无法下载的，可手动下载
* 修复部分小bug
* log计算服务的开启采用变量控制，配置文件已更新(默认关闭)

#### 2.0.4(amd)版本更新
* 修复xdd对接，登陆成功后一直转圈问题
* 去除假授权enen机制，保留假授权炸鸡机制

#### 2.0.3(amd)版本更新
* 对接xdd(配置文件已更新，配置好)
* 更换个人中心用户昵称接口
* 修复部分bug
* 身份认证出错的，带上日志和Config目录下的截图反馈

#### 2.0.2(amd)版本更新
* 修复重大bug

#### 2.0.1(amd)版本更新

* 更新二验，解决部分需要二验的账号（需要输入身份证前两位和后四位，无需分割，最后一位为X的直接写X，例如：12345X）

#### 2.0.0(amd)版本更新
* 更换登陆地址（健康社区）
* 优化授权机制
* 优化授权服务器网络
* 提高识别准确率
* 移除失效的快捷登陆接口
* 修复部分bug


## 特别声明:

* 本仓库涉仅用于测试和学习研究，禁止用于商业用途，不能保证其合法性，准确性，完整性和有效性，请根据情况自行判断.

* 本项目内所有资源文件，禁止任何公众号、自媒体进行任何形式的转载、发布。

* ht944对任何代码问题概不负责，包括但不限于由任何脚本错误导致的任何损失或损害.

* 间接使用本仓库搭建的任何用户，包括但不限于建立VPS或在某些行为违反国家/地区法律或相关法规的情况下进行传播, ht944对于由此引起的任何隐私泄漏或其他后果概不负责.

* 请勿将本项目的任何内容用于商业或非法目的，否则后果自负.

* 如果任何单位或个人认为该项目的脚本可能涉嫌侵犯其权利，则应及时通知并提供身份证明，所有权证明，我们将在收到认证文件后删除相关代码.

* 任何以任何方式查看此项目的人或直接或间接使用本仓库项目的任何脚本的使用者都应仔细阅读此声明。ht944 保留随时更改或补充此免责声明的权利。一旦使用并复制了任何本仓库项目的规则，则视为您已接受此免责声明.

**您必须在下载后的24小时内从计算机或手机中完全删除以上内容.**  </br>
> ***您使用或者复制了本仓库且本人制作的任何脚本，则视为`已接受`此声明，请仔细阅读***

## 多谢
