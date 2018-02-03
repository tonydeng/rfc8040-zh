# 1. 介绍

需要标准机制来允许`Web`应用程序以模块化和可扩展的方式访问网络设备内的配置数据，状态数据，特定于数据模型的远程过程调用（`RPC`）操作和事件通知。

本文档定义了一个基于`HTTP` [[RFC7230](https://tools.ietf.org/html/rfc7230)]的协议，称为“`RESTCONF`”，用于使用网络配置协议（`NETCONF`）中定义的数据存储概念（[RFC6241](https://tools.ietf.org/html/rfc6241)]）配置在`YANG`版本`1` [[RFC6020](https://tools.ietf.org/html/rfc6020)]或者`YANG`版本`1.1` [[RFC7950](https://tools.ietf.org/html/rfc7950)]。

`NETCONF`定义了配置数据存储和一组可用于访问这些数据存储的创建，读取，更新，删除（`CRUD`）操作。 `NETCONF`也定义了一个调用这些操作的协议。 `YANG`语言定义数据存储内容，配置，状态数据，`RPC`操作和事件通知的语法和语义。

`RESTCONF`使用`HTTP`方法在包含`YANG`定义数据的概念数据存储上提供`CRUD`操作，这与实现`NETCONF`数据存储的服务器兼容。

如果`RESTCONF`服务器与`NETCONF`服务器位于同一位置，则与`NETCONF`协议​​存在协议交互；这些交互在[1.4节](1.4.md)中描述。 `RESTCONF`服务器可以使用操作资源提供对特定数据存储的访问，如[3.6节](section-3/3.6.md)所述。 `RESTCONF`协议​​不指定任何强制操作资源。每个操作资源的语义确定是否以及如何访问数据存储。

配置数据和状态数据公开为可以使用`GET`方法检索的资源。表示配置数据的资源可以使用`DELETE`，`PATCH`，`POST`和`PUT`方法进行修改。数据使用`XML` [[W3C.REC-xml-20081126](https://tools.ietf.org/html/rfc8040#ref-W3C.REC-xml-20081126)]或`JSON` [[RFC7159](https://tools.ietf.org/html/rfc7159)]进行编码。

可以使用`POST`方法调用使用`YANG`的“`rpc`”或“`action`”语句定义的特定于数据模型的`RPC`操作。可以访问使用`YANG`“`notification`”语句定义的特定于数据模型的事件通知。
