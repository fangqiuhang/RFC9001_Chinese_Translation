---
title: "4.6. 0-RTT"
anchor: "4.6_0-RTT"
weight: 460
rank: "h2"
---

The 0-RTT feature in QUIC allows a client to send application data before the handshake is complete. This is made possible by reusing negotiated parameters from a previous connection. To enable this, 0-RTT depends on the client remembering critical parameters and providing the server with a TLS session ticket that allows the server to recover the same information.

QUIC中的0-RTT特性使得客户端可以在握手完成前就发送应用数据。这是通过重用在先前的连接中协商的参数来做到的。要启用0-RTT，要求客户端记录一些关键参数，并向服务器提供一个TLS的会话票据，这个票据使得服务器能够恢复出一份与客户端那里的相同的信息。

This information includes parameters that determine TLS state, as governed by [TLS13], QUIC transport parameters, the chosen application protocol, and any information the application protocol might need; see Section 4.6.3. This information determines how 0-RTT packets and their contents are formed.

这份信息中包含了能决定TLS状态的参数（由《[TLS13]()》管理）、QUIC传输参数、选择的应用协议和所有应用协议可能需要的信息；详见[第4.6.3章]()。这份信息决定了如何组建0-RTT数据包和其中的内容。

To ensure that the same information is available to both endpoints, all information used to establish 0-RTT comes from the same connection. Endpoints cannot selectively disregard information that might alter the sending or processing of 0-RTT.

为了确保两侧终端处的可用信息是一致的，所有用于建立0-RTT的信息均来自相同的连接。终端不能选择性地去除可能影响发送或处理0-RTT的信息。

[TLS13] sets a limit of seven days on the time between the original connection and any attempt to use 0-RTT. There are other constraints on 0-RTT usage, notably those caused by the potential exposure to replay attack; see Section 9.2.

《[TLS13]()》对于原始连接和意图使用0-RTT的连接间的时间间隔设置了7天的上限。对于0-RTT的使用还存在其他限制，尤其是那些因潜在的重放攻击风险而施加的；详见[第9.2章]()。
