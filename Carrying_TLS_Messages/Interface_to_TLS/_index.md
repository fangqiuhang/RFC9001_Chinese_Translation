---
title: "4.1. 面向TLS的接口"
anchor: "4.1_Interface_to_TLS"
weight: 410
rank: "h2"
---

如[图4](#Figure_4_QUIC_and_TLS_Interactions)所示，QUIC面向TLS的接口由四个主要函数组成：

* 发送和接收握手消息

* 处理已存储的用于恢复会话的传输状态和应用状态，并判断它们是否有效以生成或接受0-RTT数据

* 重新生成密钥（既包括发送用的也包含接收用的）

* 更新握手状态

为了配置TLS，可能需要额外的函数。尤其是，QUIC和TLS需要就哪一方负责验证对端的凭据，例如证书（详见《[RFC5280](https://www.rfc-editor.org/info/rfc5280)》），达成一致。
