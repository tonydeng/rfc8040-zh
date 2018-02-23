# 12. 安全考虑

[第2.1节](../section-2/2.1.md)指出“`RESTCONF`服务器必须支持`TLS`协议[[RFC5246](https://tools.ietf.org/html/rfc5246)]”。这种语言使得`RESTCONF`服务器也可能支持未来版本的`TLS`协议。特别需要关注的是，如[附录B.1](https://tools.ietf.org/html/rfc8040#appendix-B.1)中`TLS 1.3`文档的所述，`TLS1.3` [[TLS1.3](https://tools.ietf.org/html/draft-ietf-tls-tls13-24)]引入了对`0-RTT`握手的支持，这可能导致`RESTCONF api`的安全问题。因此，建议`RESTCONF`服务器根本不支持`0-RTT`（即使对于幂等请求也不支持），除非此`RFC`的更新指南另有规定。

[2.5节](../section-2/2.5.md)建议基于`TLS`客户端证书进行认证，但允许使用“超文本传输​​协议（`HTTP`）认证方案注册表”中定义的任何认证方案。实施需要意识到这些方法的优势差别很大，有些可能被认为是实验性的。在阅读与该方案的注册表项相关的`RFC`的安全注意事项部分之后，应该选择任何这些方案。

本备忘录中定义的“`ietf-restconf-monitoring`”`YANG`模块旨在通过`NETCONF`协议​​[[RFC6241](https://tools.ietf.org/html/rfc6241)]进行访问。`NETCONF`最底层的安全传输层强制要求使用`Secure Shell (SSH)`[[RFC6242](https://tools.ietf.org/html/rfc6242)]。`NETCONF`访问控制模型[[RFC6536](https://tools.ietf.org/html/rfc6536)]提供了将特定`NETCONF`用户的访问限制为所有可用`NETCONF`协议​​操作和内容的预配置子集的手段。

`RESTCONF`的最底层是`HTTPS`，强制实施的安全传输保障是`TLS` [[RFC5246](https://tools.ietf.org/html/rfc5246)]。 `RESTCONF`协议​​使用`NETCONF`访问控制模型[[RFC6536](https://tools.ietf.org/html/rfc6536)]，该模型提供了将特定`RESTCONF`用户的访问限制为所有可用`RESTCONF`协议​​操作和内容的预配置子集的手段。

本节提供了`RESTCONF`协议​​定义的资源的安全注意事项。 `HTTPS`的安全考虑在[[RFC7230](https://tools.ietf.org/html/rfc7230)]中定义。除了“`ietf-restconf-monitoring`”模块（[第9节](../section-9/README.md)）和“`ietf-yang-library`”模块（[第10节](../section-10/README.md)）之外，`RESTCONF`没有指定服务器需要支持哪些`YANG`模块。 `RESTCONF`操作的其他模块的安全考虑可以在定义这些`YANG`模块的文档中找到。

配置信息本质上是敏感的。它的传输清晰且没有完整性检查，让设备面临经典窃听和虚假数据注入攻击。配置信息通常包含密码，用户名，服务描述和拓扑信息，所有这些信息都很敏感。通过现有管理界面的操作实践观察到许多攻击模式。实施者在实施该协议时研究它们并考虑到它们是明智的。

不同的环境在认证之前和之后都可能允许不同的权利。当`RESTCONF`操作未被正确授权时，`RESTCONF`服务器务必返回“`401 Unauthorized`”状态行。请注意，授权信息可以以配置信息的形式交换，这是确保连接安全的更多理由。请注意，客户端可以通过监视服务器为数据存储资源返回的“`ETag`”和“`Last-Modified`”标头字段中的更改来检测其未授权访问的数据资源中的配置更改。

`RESTCONF`服务器实现应该尝试防止由于通过`POST`，`PUT`和`PATCH`方法完成编辑请求所需的过量资源消耗而导致系统中断。在这样的实现中，可能会构建一种尝试消耗所有可用内存或其他资源类型的攻击。
