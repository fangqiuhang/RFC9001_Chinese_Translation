---
title: "4.1. 面向TLS的接口"
anchor: "4.1_Interface_to_TLS"
weight: 410
rank: "h2"
---

As shown in Figure 4, the interface from QUIC to TLS consists of four primary functions:

如[图4]()所示，QUIC面向TLS的接口由四个主要函数组成：

* Sending and receiving handshake messages

* 发送和接收握手消息

* Processing stored transport and application state from a resumed session and determining if it is valid to generate or accept 0-RTT data

* 处理已存储的用于恢复会话的传输状态和应用状态，并判断它们是否有效以生成或接受0-RTT数据

* Rekeying (both transmit and receive)

* 重新生成密钥（既包括发送用的也包含接收用的）

* Updating handshake state

* 更新握手状态

Additional functions might be needed to configure TLS. In particular, QUIC and TLS need to agree on which is responsible for validation of peer credentials, such as certificate validation [RFC5280].

为了配置TLS，可能需要额外的函数。尤其是，QUIC和TLS需要就哪一方负责验证对端的凭据，例如证书（详见《[RFC5280]()》），达成一致。
