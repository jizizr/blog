---
title: Heroku搭建v2ray节点
date: 2021-08-18 14:57:59
tags:
- Heroku
- v2ray
- 节点
- 科学上网
- 翻墙
- v2
---

有一部分人觉得VPN和机场不够安全，想要自建。但是一般vps都是要花钱的。免费的vps Euserv只有ipv6的地址，warp的效果也不太理想。有没有能够免费建立节点的提供商呢？这就请到今天的主角——Heroku

## 注意事项

1. Heroku对流量检测有些严格，请避免大流量消耗
2. 免费服务请珍惜，勿滥用

## 搭建服务端

### 无caddy版 （封号概率低）

1. fork这个项目 [bclswl0827/v2ray-heroku](https://github.com/bclswl0827/v2ray-heroku)

2. 修改项目名称

3. 点击[此处](https://id.heroku.com)注册/登录账号

4. 访问 `https://dashboard.heroku.com/new?template=https://github.com/gayhub用户名/项目名`

例如：`https://dashboard.heroku.com/new?template=https://github.com/mixue/bingcheng`

5. 输入在heroku部署的App Name、uuid，点击`Deploy APP`

6. 完成在Heroku服务端的部署


### caddy版 （封号概率稍高）

1. fork这个项目 [mixool/xrayku](https://github.com/mixool/xrayku)

2. 修改项目名称

3. 点击[此处](https://id.heroku.com)注册/登录账号

4. 访问 `https://dashboard.heroku.com/new?template=https://github.com/gayhub用户名/项目名`

例如：`https://dashboard.heroku.com/new?template=https://github.com/mixue/bingcheng`

5. 输入在heroku部署的App Name、uuid，点击`Deploy APP`

6. 完成在Heroku服务端的部署

## CloudFlare 反代

1. 在[此处](https://dash.cloudflare.com)注册/登录CloudFlare（以下简称CF）账号

2. 转到workers页面

3. 创建workers

4. 把自带的代码换成下面这个

```javascript
const SingleDay = '应用程序名1.herokuapp.com'
const DoubleDay = '应用程序名2.herokuapp.com'
addEventListener(
    "fetch",event => {
    
        let nd = new Date();
        if (nd.getDate()%2) {
            host = SingleDay
        } else {
            host = DoubleDay
        }
        
        let url=new URL(event.request.url);
        url.hostname=host;
        let request=new Request(url,event.request);
        event. respondWith(
            fetch(request)
        )
    }
)
```
5. 点击`Save and deploy`

6. 记录下workers的三级域名

## 配置教程

1. 打开v2rayN或其他客户端

2. 新建一个vmess服务器

3. 参考以下信息配置

### 无caddy版

地址：`cf优选ip`
端口：`443`
uuid：`你设置的uuid`
额外id：`64`
加密方式：`auto`
别名：`自行命名`
传输协议：`ws`
底层传输安全：`tls`
伪装类型：`none`
伪装域名：`你的workers域名`
SNI：`你的workers域名`
路径：`/`

### caddy版

地址：`cf优选ip`
端口：`443`
uuid：`你设置的uuid`
额外id：`0`
加密方式：`auto`
别名：`自行命名`
传输协议：`ws`
底层传输安全：`tls`
伪装类型：`none`
伪装域名：`你的workers域名`
SNI：`你的workers域名`
路径：`/你设置的uuid-vmess`

4. 测试连接，大功告成

