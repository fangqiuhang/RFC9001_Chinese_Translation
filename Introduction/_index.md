---
title: "1. 介绍"
anchor: "1_Introduction"
weight: 100
rank: "h1"
---

This document describes how QUIC [QUIC-TRANSPORT] is secured using TLS [TLS13].

本文档描述了如何使用TLS（详见《[TLS13]()》）来加固QUIC（详见《[QUIC传输]()》）的安全性。

TLS 1.3 provides critical latency improvements for connection establishment over previous versions. Absent packet loss, most new connections can be established and secured within a single round trip; on subsequent connections between the same client and server, the client can often send application data immediately, that is, using a zero round-trip setup.

TLS 1.3比起之前的版本，为连接建立提供了延迟方面重要的性能提升。在没有数据包丢包的情况下，绝大多数新连接都能够在单次往返时间内得到建立和加固；当相同客户端和服务器间进行后续连接时，客户端通常可以立即发送应用数据，也就是，使用零往返启动来进行连接。

This document describes how TLS acts as a security component of QUIC.

本文档描述了TLS作为QUIC的安全组件时是如何工作的。
