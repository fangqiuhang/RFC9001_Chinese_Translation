---
title: "5.4. 头部保护"
anchor: "5.4_Header_Protection"
weight: 540
rank: "h2"
---

Parts of QUIC packet headers, in particular the Packet Number field, are protected using a key that is derived separately from the packet protection key and IV. The key derived using the "quic hp" label is used to provide confidentiality protection for those fields that are not exposed to on-path elements.

QUIC数据包头部的一部分，尤其是数据包号字段，会受到独立衍生自数据包保护密钥和IV的密钥的保护。使用值为`quic hp`的标签衍生的密钥被用于对那些没有暴露给路径上设备的字段提供可信度保护。

This protection applies to the least significant bits of the first byte, plus the Packet Number field. The four least significant bits of the first byte are protected for packets with long headers; the five least significant bits of the first byte are protected for packets with short headers. For both header forms, this covers the reserved bits and the Packet Number Length field; the Key Phase bit is also protected for packets with a short header.

这项保护应用于首个字节的几个最低有效位，以及数据包号字段。对于长包头数据包，首个字节的四个最低有效位会受到保护；对于短包头数据包，首个字节的五个最低有效位会受到保护。不管是哪种形式的头部，都会覆盖到保留位和数据包号长度字段；短包头数据包的密钥阶段比特位也会受到保护。

The same header protection key is used for the duration of the connection, with the value not changing after a key update (see Section 6). This allows header protection to be used to protect the key phase.

在连接期间，使用的头部保护密钥保持不变，即便是在经过密钥更新后（详见[第6章]()）。这使得头部保护可以被用来保护密钥阶段。

This process does not apply to Retry or Version Negotiation packets, which do not contain a protected payload or any of the fields that are protected by this process.

头部保护的过程不适用于重试数据包或版本协商数据包，这类数据包不包含受保护的载荷或任何会被此过程保护的字段。
