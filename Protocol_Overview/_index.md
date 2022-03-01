---
title: "3. 协议概述"
anchor: "3_Protocol_Overview"
weight: 300
rank: "h1"
---

QUIC [QUIC-TRANSPORT] assumes responsibility for the confidentiality and integrity protection of packets. For this it uses keys derived from a TLS handshake [TLS13], but instead of carrying TLS records over QUIC (as with TCP), TLS handshake and alert messages are carried directly over the QUIC transport, which takes over the responsibilities of the TLS record layer, as shown in Figure 3.

QUIC（详见《[QUIC传输]()》）负责数据包的可信度和完整性保护。为此它使用了衍生自TLS握手（详见《[TLS13]()》）的密钥，但如[图3]()所示，TLS握手和警告消息由QUIC传输层直接传递，而不是在QUIC传输层的基础上使用TLS记录来传递（TCP是这么做的），也就是说QUIC接管了TLS记录层的职责。

> TODO：图3

{{< block_img
indx="Figure_3_QUIC_Layers"
title="图3：QUIC的层"
type="svg"
src="/RFC9000_Chinese_Translation/images/Figure_2_States_for_Sending_Parts_of_Streams.svg" >}}

QUIC also relies on TLS for authentication and negotiation of parameters that are critical to security and performance.

QUIC还依靠TLS来验证和协商那些安全和性能方面的关键参数。

Rather than a strict layering, these two protocols cooperate: QUIC uses the TLS handshake; TLS uses the reliability, ordered delivery, and record layer provided by QUIC.

这两种协议间没有严格的层次区分，取而代之的是它们相互合作：QUIC使用TLS的握手；TLS使用由QUIC提供的可靠性、有序交付和记录层等特性。

At a high level, there are two main interactions between the TLS and QUIC components:

抽象地说，TLS组件和QUIC组件间主要有两类交互：

* The TLS component sends and receives messages via the QUIC component, with QUIC providing a reliable stream abstraction to TLS.

* TLS组件经由QUIC组件发送和接收消息，QUIC向TLS提供一种可靠的流的抽象。

* The TLS component provides a series of updates to the QUIC component, including (a) new packet protection keys to install and (b) state changes such as handshake completion, the server certificate, etc.

* TLS组件向QUIC组件提供一系列状态更新，包括(a)新的数据包保护密钥，和(b)状态变更，例如握手完成、服务器证书，等等。

Figure 4 shows these interactions in more detail, with the QUIC packet protection being called out specially.

[图4]()更详细地展示了这些交互，并且把QUIC数据包保护单独提了出来。

> TODO：图4

{{< block_img
indx="Figure_4_QUIC_and_TLS_Interactions"
title="图4：QUIC和TLS的交互"
type="svg"
src="/RFC9000_Chinese_Translation/images/Figure_2_States_for_Sending_Parts_of_Streams.svg" >}}

Unlike TLS over TCP, QUIC applications that want to send data do not send it using TLS Application Data records. Rather, they send it as QUIC STREAM frames or other frame types, which are then carried in QUIC packets.

不像基于TCP的TLS，想要发送数据的QUIC应用并不使用TLS应用数据记录来发送，而是将数据以QUIC**流帧**或其他类型的帧的形式发送，它们都是由QUIC数据包传递的。
