---
title: "4. 传递TLS消息"
anchor: "4_Carrying_TLS_Messages"
weight: 400
rank: "h1"
---

QUIC carries TLS handshake data in CRYPTO frames, each of which consists of a contiguous block of handshake data identified by an offset and length. Those frames are packaged into QUIC packets and encrypted under the current encryption level. As with TLS over TCP, once TLS handshake data has been delivered to QUIC, it is QUIC's responsibility to deliver it reliably. Each chunk of data that is produced by TLS is associated with the set of keys that TLS is currently using. If QUIC needs to retransmit that data, it MUST use the same keys even if TLS has already updated to newer keys.

QUIC用**加密帧**中传递TLS握手数据，每个帧由一些连续的握手数据块组成，并使用偏移值和长度值来区分数据块。这些帧被封装进QUIC数据包并受到当前密级的加密。就像基于TCP的TLS一样，一旦TLS握手数据被交付给QUIC，QUIC就有责任将数据可靠地交付给对方。每一份由TLS生成的数据分块都被关联到TLS正在使用的一组密钥。如果QUIC需要重传某份数据，那么它{{< req_level MUST >}}使用相同的密钥，哪怕TLS已经改用更新的密钥了。

Each encryption level corresponds to a packet number space. The packet number space that is used determines the semantics of frames. Some frames are prohibited in different packet number spaces; see Section 12.5 of [QUIC-TRANSPORT].

每个密级对应这一个数据包号空间。正在使用的数据包号空间决定了帧的语义。在特定的数据包号空间里，有些帧是被禁止使用的；详见《[QUIC传输]()》的[第12.5章]()。

Because packets could be reordered on the wire, QUIC uses the packet type to indicate which keys were used to protect a given packet, as shown in Table 1. When packets of different types need to be sent, endpoints SHOULD use coalesced packets to send them in the same UDP datagram.

由于数据包在链路上可能出现乱序，QUIC使用数据包类型来表明用于保护给定数据包的密钥，如[表1]()所示。当要发送不同类型的数据包时，终端{{< req_level SHOULD >}}使用合并数据包的方法从而在单个UDP数据报中发送它们。

Table 1: Encryption Keys by Packet Type
Packet Type	Encryption Keys	PN Space
Initial	Initial secrets	Initial
0-RTT Protected	0-RTT	Application data
Handshake	Handshake	Handshake
Retry	Retry	N/A
Version Negotiation	N/A	N/A
Short Header	1-RTT	Application data

{{% block_ref
indx="Table_1_Encryption_Keys_by_Packet_Type"
title="表1：数据包类型对应的加密密钥" %}}

| 数据包类型     | 加密密钥  | 数据包号空间           |
|:----------|:------|:-----------------|
| **初始**    | 初始秘密值 | 初始               |
| **0-RTT** | 0-RTT | Application data |
| **握手**    | 握手    | 握手               |
| **重试**    | 重试    | 不适用              |
| **版本协商**  | 不适用   | 不适用              |
| **短包头**   | 1-RTT | 应用数据             |

{{% /block_ref %}}

Section 17 of [QUIC-TRANSPORT] shows how packets at the various encryption levels fit into the handshake process.

《[QUIC传输]()》的[第17章]()描述了各种密级的数据包如何参与握手过程。
