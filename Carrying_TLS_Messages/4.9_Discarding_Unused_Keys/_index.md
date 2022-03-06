---
title: "4.9. 丢弃不再使用的密钥"
anchor: "4.9_Discarding_Unused_Keys"
weight: 490
rank: "h2"
---

After QUIC has completed a move to a new encryption level, packet protection keys for previous encryption levels can be discarded. This occurs several times during the handshake, as well as when keys are updated; see Section 6.

在QUIC移动到新的密级后，先前密级的数据包保护密钥就可以被弃用。这会在握手过程中以及密钥被更新时发生数次，详见[第6章]()。

Packet protection keys are not discarded immediately when new keys are available. If packets from a lower encryption level contain CRYPTO frames, frames that retransmit that data MUST be sent at the same encryption level. Similarly, an endpoint generates acknowledgments for packets at the same encryption level as the packet being acknowledged. Thus, it is possible that keys for a lower encryption level are needed for a short time after keys for a newer encryption level are available.

当新的数据包保护密钥可用时，先前的密钥不会被立即弃用。如果有处于较低密级的数据包包含着**加密帧**，那么用于重传其中数据的新帧{{< req_level MUST >}}使用相同密级发送。类似地，在确认这个较低密级的数据包时，终端要为这个密级的数据包创建确认。因此，在新密级密钥可用后的短暂时间内需要较低密级的密钥的情况是有可能出现的。

An endpoint cannot discard keys for a given encryption level unless it has received all the cryptographic handshake messages from its peer at that encryption level and its peer has done the same. Different methods for determining this are provided for Initial keys (Section 4.9.1) and Handshake keys (Section 4.9.2). These methods do not prevent packets from being received or sent at that encryption level because a peer might not have received all the acknowledgments necessary.

终端只有从对端收到了某个密级的所有加密握手消息并且对端也收到了所有相应消息时，才能弃用这个密级的密钥。要判断这一点，初始密钥和握手密钥使用不同的方法（详见[第4.9.1章]()和[第4.9.2章]()）。这些方法不会阻止数据包在某个密级上的发送与接收，因为对端可能还没有接收完所有必需的确认。

Though an endpoint might retain older keys, new data MUST be sent at the highest currently available encryption level. Only ACK frames and retransmissions of data in CRYPTO frames are sent at a previous encryption level. These packets MAY also include PADDING frames.

尽管终端可以持续保留旧的密钥，但是新数据{{< req_level MUST >}}使用当前可用的最高密级来发送。只有**ACK帧**和重传数据的**加密帧**会使用先前的密级来发送。这些数据包中还{{< req_level MAY >}}包含**填充帧**。
