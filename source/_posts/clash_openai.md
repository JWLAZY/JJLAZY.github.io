---
title: ChatGPT指定节点访问
tags: ChatGPT
date: 2023-06-27
---
OpenAI风控太厉害了，第一个账号因为一直切换IP所有被封号了, 后来每次使用ChatGPT的时候都需要确认IP使用美国直连的节点。

但是还是太麻烦了，今天研究了下clash客户端的规则，风险使用配置文件可以很轻松的实现使用OpenAI时走固定节点，而且其他域名走其他节点。

步骤如下：

1. 使用proxy-provider模式

   ```
    proxy-providers:
      agentProxy:
        type: http
        path: ./profiles/xxx.yml
        url: https://xxx/clash_proxies.yml
        interval: 36000
        health-check:
          enable: true
          url: http://www.gstatic.com/generate_204
          interval: 3600
      usa:
        type: file
        path: ./profiles/usa-only.yml
        interval: 36000
        health-check:
          enable: true
          url: http://www.gstatic.com/generate_204
          interval: 3600
   ```
   第一个为订阅模式，会自拉取节点到 ./profiles/xxx.yml中。
   第二个是本地文件模式，可以把第一个订阅的节点写到第二个配置文件中。
   这样节点就配置好了。
2. 配置proxy-groups
```
  # 代理组策略
  proxy-groups:
  - name: PROXY-USA
    type: select
    use:
    - usa
  - name: PROXY
    type: select
    use:
    - agentProxy
```
相当于定义了两个代理组，第一个组中只有美国节点。
3. 配置rules
```
  rules:
  # CUSTOM
  - DOMAIN-SUFFIX,openai.com,PROXY-USA
```
这样的话，openai的流量就只会走美国节点了。
看下clash的日志
```
[2023-06-27 17:32:17][INFO] [TCP] 127.0.0.1:65228 --> in.appcenter.ms:443 match Match() using FINAL[x1.0 香港 - 中转1]
[2023-06-27 17:32:24][INFO] [TCP] 127.0.0.1:65247 --> collector.github.com:443 match Match() using FINAL[x1.0 香港 - 中转1]
[2023-06-27 17:32:28][INFO] [TCP] 127.0.0.1:65264 --> openaiapi-site.azureedge.net:443 match Match() using FINAL[x1.0 香港 - 中转1]
[2023-06-27 17:32:28][INFO] [TCP] 127.0.0.1:65265 --> fonts.googleapis.com:443 match DomainKeyword(google) using PROXY[x1.0 香港 - 中转1]
[2023-06-27 17:32:28][INFO] [TCP] 127.0.0.1:65262 --> platform.openai.com:443 match DomainSuffix(openai.com) using PROXY-USA[x1.0 美西 - 直连1]
[2023-06-27 17:32:28][INFO] [TCP] 127.0.0.1:65263 --> beta.openai.com:443 match DomainSuffix(openai.com) using PROXY-USA[x1.0 美西 - 直连1]
[2023-06-27 17:32:29][INFO] [TCP] 127.0.0.1:65274 --> fonts.gstatic.com:443 match DomainSuffix(gstatic.com) using PROXY[x1.0 香港 - 中转1]
[2023-06-27 17:32:29][INFO] [TCP] 127.0.0.1:65273 --> cdn.openai.com:443 match DomainSuffix(openai.com) using PROXY-USA[x1.0 美西 - 直连1]
[2023-06-27 17:32:30][INFO] [TCP] 127.0.0.1:65282 --> openaiapi-site.azureedge.net:443 match Match() using FINAL[x1.0 香港 - 中转1]
[2023-06-27 17:32:30][INFO] [TCP] 127.0.0.1:65279 --> api.openai.com:443 match DomainSuffix(openai.com) using PROXY-USA[x1.0 美西 - 直连1]
[2023-06-27 17:32:32][INFO] [TCP] 127.0.0.1:65290 --> widget.intercom.io:443 match Match() using FINAL[x1.0 香港 - 中转1]
[2023-06-27 17:32:49][INFO] [TCP] 127.0.0.1:65340 --> exp.notion.so:443 match DomainSuffix(notion.so) using PROXY[x1.0 香港 - 中转1]
```

ok, 之前一直没有仔细的看clash的文档，今天研究下，发现可以搞的事情还有很多！
