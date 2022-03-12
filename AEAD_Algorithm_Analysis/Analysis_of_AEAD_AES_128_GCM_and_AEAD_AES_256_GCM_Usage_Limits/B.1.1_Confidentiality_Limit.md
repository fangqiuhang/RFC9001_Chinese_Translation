---
title: "B.1.1. 可信度上限"
anchor: "B.1.1_Confidentiality_Limit"
weight: 1311
rank: "h3"
---

For confidentiality, Theorem (4.3) in [GCM-MU] establishes that, for a single user that does not repeat nonces, the dominant term in determining the distinguishing advantage between a real and random AEAD algorithm gained by an attacker is:

在可信度方面，《[GCM-MU]()》中的定理4.3指出，对于一个不会重复随机数的用户，计算攻击者随机选择的AEAD算法相比实际使用的真实AEAD算法的优势程度的表达式为：

{{% block_ref
indx="Pseudocode_B_1_1_1" %}}

```
2 * (q * l)^2 / 2^n
```

{{% /block_ref %}}

For a target advantage of 2-57, this results in the relation:

当目标优势度为<code>2<sup>-57</sup></code>时，会得到这样的关系：

{{% block_ref
indx="Pseudocode_B_1_1_2" %}}

```
q <= 2^35 / l
```

{{% /block_ref %}}

Thus, endpoints that do not send packets larger than 211 bytes cannot protect more than 228 packets in a single connection without causing an attacker to gain a more significant advantage than the target of 2-57. The limit for endpoints that allow for the packet size to be as large as 216 is instead 223.

因此，发送不超过<code>2<sup>11</sup></code>字节的数据包的终端无法在单条连接中保护<code>2<sup>28</sup></code>个以上的数据包却不让攻击者获得超过<code>2<sup>-57</sup></code>优势度。对于允许数据包尺寸达到<code>2<sup>16</sup></code>字节的终端，则该限制为<code>2<sup>23</sup></code>个数据包。
