---
title: "B.2. 对于AEAD_AES_128_CCM用量上限的分析"
anchor: "B.2_Analysis_of_AEAD_AES_128_CCM_Usage_Limits"
weight: 1320
rank: "h2"
---

TLS（详见《[TLS13](https://www.rfc-editor.org/info/rfc8446)》）和《[AEBounds](https://www.isg.rhul.ac.uk/~kp/TLS-AEbounds.pdf)》都没有为`AEAD_AES_128_CCM`的用量设定上限。然而，任何与QUIC一起使用的AEAD都需要在用量上设定上限以确保可信度和完整性都能得到维持。本节记述了关于此上限的分析。

《[CCM-ANALYSIS](https://doi.org/10.1007/3-540-36492-7_7)》被用作本分析的基础。该文献中的分析结果被用于计算用量上限。

在可信度方面，《[CCM-ANALYSIS](https://doi.org/10.1007/3-540-36492-7_7)》中的定理2指出，攻击者相比理想的伪随机排列（PRP）获得的优势不会超过此值：

{{% block_ref
indx="Pseudocode_B_2_1" %}}

```
(2l * q)^2 / 2^n
```

{{% /block_ref %}}

在相同消息数量的情况下，《[CCM-ANALYSIS](https://doi.org/10.1007/3-540-36492-7_7)》中的定理1中的完整性上限给予了攻击者更多优势。由于可信度方面优势与完整性方面优势的目标值是相同的，所以只需要考虑定理1。

定理1指出，攻击者相比理想的PRP获得的优势不会超过此值：

{{% block_ref
indx="Pseudocode_B_2_2" %}}

```
v / 2^t + (2l * (v + q))^2 / 2^n
```

{{% /block_ref %}}

由于`t`和`n`都是`128`，第一项相比第二项变得微不足道，因此第一项可以被移除而不会对结果产生重要影响。

这产生了一种关系，它将加密尝试次数和解密尝试次数关联到了相同的上限值上，这个上限值是定理为可信度生成的。当目标优势度为<code>2<sup>-57</sup></code>时，这会产生以下结果：

{{% block_ref
indx="Pseudocode_B_2_3" %}}

```
v + q <= 2^34.5 / l
```

{{% /block_ref %}}

通过设置`q = v`，可信度上限和完整性上限的值就都能被推导出来。因此限制数据包尺寸不超过<code>2<sup>11</sup></code>字节的终端使用<code>2<sup>26.5</sup></code>个数据包的可信度上限和完整性上限。不限制数据包尺寸的终端则使用值为<code>2<sup>21.5</sup></code>的上限。
