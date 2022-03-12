---
title: "B.1.2. 完整性上限"
anchor: "B.1.2_Integrity_Limit"
weight: 1312
rank: "h3"
---

For integrity, Theorem (4.3) in [GCM-MU] establishes that an attacker gains an advantage in successfully forging a packet of no more than the following:

在完整性方面，《[GCM-MU]()》中的定理4.3指出，攻击者在伪造数据包时次数不需要超过此值就能获得明显优势：

{{% block_ref
indx="Pseudocode_B_1_2_1" %}}

```
(1 / 2^(8 * n)) + ((2 * v) / 2^(2 * n))
        + ((2 * o * v) / 2^(k + n)) + (n * (v + (v * l)) / 2^k)
```

{{% /block_ref %}}

The goal is to limit this advantage to 2-57. For AEAD_AES_128_GCM, the fourth term in this inequality dominates the rest, so the others can be removed without significant effect on the result. This produces the following approximation:

我们的目标是将此优势限制到<code>2<sup>-57</sup></code>以下。对于`AEAD_AES_128_GCM`，不等式中的第四项占据主导地位，所以其余项可以被移除而不会对结果产生重要影响。这会产生以下近似结果：

{{% block_ref
indx="Pseudocode_B_1_2_2" %}}

```
v <= 2^64 / l
```

{{% /block_ref %}}

Endpoints that do not attempt to remove protection from packets larger than 211 bytes can attempt to remove protection from at most 257 packets. Endpoints that do not restrict the size of processed packets can attempt to remove protection from at most 252 packets.

不会尝试对超过<code>2<sup>11</sup></code>字节的数据包移除保护的终端最多可以尝试为<code>2<sup>57</sup></code>个数据包移除保护。并不限制所处理的数据包尺寸的终端最多可以尝试为<code>2<sup>52</sup></code>个数据包移除保护。

For AEAD_AES_256_GCM, the same term dominates, but the larger value of k produces the following approximation:

对于`AEAD_AES_256_GCM`，占据主导地位的是同一项，但是较大的`k`值会产生以下近似结果：

{{% block_ref
indx="Pseudocode_B_1_2_3" %}}

```
v <= 2^192 / l
```

{{% /block_ref %}}

This is substantially larger than the limit for AEAD_AES_128_GCM. However, this document recommends that the same limit be applied to both functions as either limit is acceptably large.

这比对`AEAD_AES_128_GCM`的限制要大得多。但是，本文档建议对两个函数施加同样的限制，因为任一限制都是可接受且足够大的。
