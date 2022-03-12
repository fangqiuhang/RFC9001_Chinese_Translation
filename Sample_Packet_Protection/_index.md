---
title: "附录A. 数据包保护样例"
anchor: "Appendix_A_Sample_Packet_Protection"
weight: 1200
rank: "h1"
---

This section shows examples of packet protection so that implementations can be verified incrementally. Samples of Initial packets from both client and server plus a Retry packet are defined. These packets use an 8-byte client-chosen Destination Connection ID of 0x8394c8f03e515708. Some intermediate values are included. All values are shown in hexadecimal.

本章展示了数据包保护的一些例子，以便于QUIC的实现可以逐步验证自己的计算结果。这里为客户端和服务器分别定义了初始数据包的样例，以及一个重试数据包。这些数据包使用了一个由客户端选择的8字节长的目标连接ID，其值为`0x8394c8f03e515708`。样例中还包含了计算过程的一些中间值。所有值都是以十六进制表示的。
