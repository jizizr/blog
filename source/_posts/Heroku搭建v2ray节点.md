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

## 搭建方法

### 无caddy版 （封号概率低）

1. fork这个项目 [bclswl0827/v2ray-heroku](https://github.com/bclswl0827/v2ray-heroku)