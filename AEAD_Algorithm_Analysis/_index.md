---
title: "附录B. AEAD算法分析"
anchor: "Appendix_B_AEAD_Algorithm_Analysis"
weight: 1300
rank: "h1"
---

This section documents analyses used in deriving AEAD algorithm limits for AEAD_AES_128_GCM, AEAD_AES_128_CCM, and AEAD_AES_256_GCM. The analyses that follow use symbols for multiplication (*), division (/), and exponentiation (^), plus parentheses for establishing precedence. The following symbols are also used:

本章记述了在为`AEAD_AES_128_GCM`、`AEAD_AES_128_CCM`和`AEAD_AES_256_GCM`计算AEAD算法的用量上限时使用的分析方法。在下文的分析中，使用了乘法运算符号（`*`）、除法运算符号（`/`）和幂运算符号（`^`），并使用括号来指定优先级。除此之外，还使用了以下符号：

t:
The size of the authentication tag in bits. For these ciphers, t is 128.

`t`：

:   认证标签以比特为单位的长度。对于以上加密算法，`t`的值为`128`。

n:
The size of the block function in bits. For these ciphers, n is 128.

`n`：

:   块函数以比特位单位的长度。对于以上算法，`n`的值为`128`。

k:
The size of the key in bits. This is 128 for AEAD_AES_128_GCM and AEAD_AES_128_CCM; 256 for AEAD_AES_256_GCM.

`k`：

:   密钥以比特为单位的长度。对于`AEAD_AES_128_GCM`和`AEAD_AES_128_CCM`，`n`的值为`128`；`AEAD_AES_256_GCM`则为256。

l:
The number of blocks in each packet (see below).

`l`：

:   每个数据包中块的数量（见下文）。

q:
The number of genuine packets created and protected by endpoints. This value is the bound on the number of packets that can be protected before updating keys.

`q`：

:   终端创建和保护的真实数据包的数量。这个值的上限为终端在更新密钥前能够保护的数据包数量。

v:
The number of forged packets that endpoints will accept. This value is the bound on the number of forged packets that an endpoint can reject before updating keys.

`v`：

:   终端接受的伪造数据包的数量。这个值的上限为终端在更新密钥前能够拒绝的伪造数据包的数量。

o:
The amount of offline ideal cipher queries made by an adversary.

`o`：

:   攻击者离线进行的理想加密查询次数。

The analyses that follow rely on a count of the number of block operations involved in producing each message. This analysis is performed for packets of size up to 211 (l = 27) and 216 (l = 212). A size of 211 is expected to be a limit that matches common deployment patterns, whereas the 216 is the maximum possible size of a QUIC packet. Only endpoints that strictly limit packet size can use the larger confidentiality and integrity limits that are derived using the smaller packet size.

下文的分析依赖于在创建各条消息时对块操作进行计数。该分析是对尺寸不超过<code>2<sup>11</sup></code>（`l`为<code>2<sup>27</sup></code>）或<code>2<sup>16</sup></code>（`l`为<code>2<sup>12</sup></code>）的数据包进行的。<code>2<sup>11</sup></code>这个尺寸应该是一个与常见部署模式匹配的上限值，而<code>2<sup>16</sup></code>是单个QUIC数据包的所有可能的尺寸中的最大值。只有严格限制数据包尺寸的终端才能使用通过较小的数据包尺寸计算出的较大的那组可信度和完整性上限。

For AEAD_AES_128_GCM and AEAD_AES_256_GCM, the message length (l) is the length of the associated data in blocks plus the length of the plaintext in blocks.

对于`AEAD_AES_128_GCM`和`AEAD_AES_256_GCM`，消息长度（`l`）是块中关联数据的长度与块中明文的长度之和。

For AEAD_AES_128_CCM, the total number of block cipher operations is the sum of the following: the length of the associated data in blocks, the length of the ciphertext in blocks, the length of the plaintext in blocks, plus 1. In this analysis, this is simplified to a value of twice the length of the packet in blocks (that is, 2l = 28 for packets that are limited to 211 bytes, or 2l = 213 otherwise). This simplification is based on the packet containing all of the associated data and ciphertext. This results in a one to three block overestimation of the number of operations per packet.

对于`AEAD_AES_128_CCM`，块加密操作的总数为以下项目的总和：关联数据以块为单位的长度、密文以块为单位的长度和明文以块为单位的长度，最后再加上1。在本分析中，这个值被简化为数据包以块为单位的长度的两倍（也就是说，对于尺寸上限为<code>2<sup>11</sup></code>的数据包，`2l`为<code>2<sup>8</sup></code>，否则`2l`为<code>2<sup>13</sup></code>）。这种简化是基于包含全部关联数据和密文的数据包的。它会造成对于每个数据包中的操作数量会多计算一至三个块。
