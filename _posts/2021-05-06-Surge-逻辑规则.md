---
layout:     post
title:      "Surge | 规则：逻辑规则"
subtitle:   "Surge 逻辑规则简单示例"
date:       2021-05-06
author:     "MAICOO"
header-img: "img/post-bg-surge.jpg"
catalog: true
tags:
    - Surge
    - 规则
    - 逻辑规则
---

### AND
> 与规则 - 当所有子规则都满足时，则执行该规则：

```
AND,((#Rule1), (#Rule2), (#Rule3)...),Proxy
```
*示例*
```
AND,((PROCESS-NAME,Google Chrome),(PROTOCOL,UDP)),REJECT
```
拦截 Chrome 发出的 UDP 数据包。

### OR
> 或规则 - 当任意子规则满足时，则执行该规则：

```
OR,((#Rule1), (#Rule2), (#Rule3)...),Proxy
```
*示例*
```
OR,((RULE-SET,SYSTEM), (RULE-SET,LAN), (GEOIP,CN)),DIRECT
```
Surge 系统内置规则可以用 OR 规则写到一条内，表示系统内置规则 SYSTEM、本地局域网、GeoIP 中国走直连。

### NOT
> 非规则 - 当任意子规则满足时，则执行该规则：

```
NOT,((#Rule1)),Proxy
```
*示例*
```
AND,((NOT,((SRC-IP,192.168.1.110))),(DOMAIN, example.com)),DIRECT
```
这条规则稍微有点复杂，它将 AND 和 NOT 相结合，它表示网关模式下除了设备 192.168.1.110 以外的其他设备在请求域名 example.com 时做直连处理。