---
title: "B.2. 对于AEAD_AES_128_CCM用量上限的分析"
anchor: "B.2_Analysis_of_AEAD_AES_128_CCM_Usage_Limits"
weight: 1320
rank: "h2"
---

TLS [TLS13] and [AEBounds] do not specify limits on usage for AEAD_AES_128_CCM. However, any AEAD that is used with QUIC requires limits on use that ensure that both confidentiality and integrity are preserved. This section documents that analysis.

TLS（详见《[TLS13]()》）和《[AEBounds]()》都没有为`AEAD_AES_128_CCM`的用量设定上限。然而，任何与QUIC一起使用的AEAD都需要在用量上设定上限以确保可信度和完整性都能得到维持。本节记述了关于此上限的分析。

[CCM-ANALYSIS] is used as the basis of this analysis. The results of that analysis are used to derive usage limits that are based on those chosen in [TLS13].

《[CCM-ANALYSIS]()》被用作本分析的基础。该文献中的分析结果被用于计算用量上限。

For confidentiality, Theorem 2 in [CCM-ANALYSIS] establishes that an attacker gains a distinguishing advantage over an ideal pseudorandom permutation (PRP) of no more than the following:

在可信度方面，《[CCM-ANALYSIS]()》中的定理2指出，攻击者相比理想的伪随机排列（PRP）获得的优势不会超过此值：

{{% block_ref
indx="Pseudocode_B_2_1" %}}

```
(2l * q)^2 / 2^n
```

{{% /block_ref %}}

The integrity limit in Theorem 1 in [CCM-ANALYSIS] provides an attacker a strictly higher advantage for the same number of messages. As the targets for the confidentiality advantage and the integrity advantage are the same, only Theorem 1 needs to be considered.

在相同消息数量的情况下，《[CCM-ANALYSIS]()》中的定理1中的完整性上限给予了攻击者更多优势。由于可信度方面优势与完整性方面优势的目标值是相同的，所以只需要考虑定理1。

Theorem 1 establishes that an attacker gains an advantage over an ideal PRP of no more than the following:

定理1指出，攻击者相比理想的PRP获得的优势不会超过此值：

{{% block_ref
indx="Pseudocode_B_2_2" %}}

```
v / 2^t + (2l * (v + q))^2 / 2^n
```

{{% /block_ref %}}

As t and n are both 128, the first term is negligible relative to the second, so that term can be removed without a significant effect on the result.

由于`t`和`n`都是`128`，第一项相比第二项变得微不足道，因此第一项可以被移除而不会对结果产生重要影响。

This produces a relation that combines both encryption and decryption attempts with the same limit as that produced by the theorem for confidentiality alone. For a target advantage of 2-57, this results in the following:

这产生了一种关系，它将加密尝试次数和解密尝试次数关联到了相同的上限值上，这个上限值是定理为可信度生成的。当目标优势度为<code>2<sup>-57</sup></code>时，这会产生以下结果：

{{% block_ref
indx="Pseudocode_B_2_3" %}}

```
v + q <= 2^34.5 / l
```

{{% /block_ref %}}

By setting q = v, values for both confidentiality and integrity limits can be produced. Endpoints that limit packets to 211 bytes therefore have both confidentiality and integrity limits of 226.5 packets. Endpoints that do not restrict packet size have a limit of 221.5.

通过设置`q = v`，可信度上限和完整性上限的值就都能被推导出来。因此限制数据包尺寸不超过<code>2<sup>11</sup></code>字节的终端使用<code>2<sup>26.5</sup></code>个数据包的可信度上限和完整性上限。不限制数据包尺寸的终端则使用值为<code>2<sup>21.5</sup></code>的上限。
