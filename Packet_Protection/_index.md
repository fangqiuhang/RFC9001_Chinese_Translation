---
title: "5. 数据包保护"
anchor: "5_Packet_Protection"
weight: 500
rank: "h1"
---

As with TLS over TCP, QUIC protects packets with keys derived from the TLS handshake, using the AEAD algorithm [AEAD] negotiated by TLS.

就像基于TCP的TLS一样，QUIC用衍生自TLS握手的密钥来保护数据包，使用的是由TLS协商的AEAD算法（详见《[AEAD]()》）。

QUIC packets have varying protections depending on their type:

QUIC数据包的保护方法视数据包类型而定：

* Version Negotiation packets have no cryptographic protection.

* 版本协商数据包不受加密保护。

* Retry packets use AEAD_AES_128_GCM to provide protection against accidental modification and to limit the entities that can produce a valid Retry; see Section 5.8.

* 重试数据包使用`AEAD_AES_128_GCM`来提供保护以免受到意外修改，并且限制能够构造合法重试数据包的实体；详见[第5.8章]()。

* Initial packets use AEAD_AES_128_GCM with keys derived from the Destination Connection ID field of the first Initial packet sent by the client; see Section 5.2.

* 初始数据包使用`AEAD_AES_128_GCM`和衍生自客户端发送的首个初始数据包的目标连接ID字段的密钥；详见[第5.2章]()。

* All other packets have strong cryptographic protections for confidentiality and integrity, using keys and algorithms negotiated by TLS.

* 所有其他类型的数据包在可信度和完整性上都受到健壮的加密保护，使用的是由TLS协商的密钥和加密算法。

This section describes how packet protection is applied to Handshake packets, 0-RTT packets, and 1-RTT packets. The same packet protection process is applied to Initial packets. However, as it is trivial to determine the keys used for Initial packets, these packets are not considered to have confidentiality or integrity protection. Retry packets use a fixed key and so similarly lack confidentiality and integrity protection.

本章描述了怎样将数据包保护应用到握手数据包、0-RTT数据包和1-RTT数据包上。同样的数据包保护过程还会被应用到初始数据包上。然而，由于决定用于初始数据包的密钥的过程是公开的，所以这类数据包不被认为受到可信度和完整性保护。类似地，重试数据包使用了固定密钥所以也缺乏可信度和完整性保护。
