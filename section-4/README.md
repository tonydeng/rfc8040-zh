# 4. `RESTCONF`方法

`RESTCONF`协议使用`HTTP`方法来标识为特定资源请求的`CRUD`操作。

下表显示了`RESTCONF`操作如何与`NETCONF`协议操作相关。

| RESTCONF | NETCONF  |
| :------------- | :------------- |
| OPTIONS       | none |
| HEAD       | `<get-config>`, `<get>` |
| GET       | `<get-config>`, `<get>`       |
| POST       | `<edit-config>` (nc:operation="create") |
| POST       | invoke an RPC operation |
| PUT       | `<copy-config>` (PUT on datastore) |
| PUT       | `<edit-config>` (nc:operation="create/replace") |
| PATCH       | `<edit-config>` (nc:operation depends on PATCH content) |
| DELETE       | `<edit-config>` (nc:operation="delete") |

`HTTP` `DELETE`方法不支持`NETCONF` `<edit-config>` `RPC`操作的“`remove`”编辑操作属性。 资源必须存在，否则`DELETE`方法将失败。 `PATCH`方法相当于使用普通补丁时的“`merge`”编辑操作（参见[第4.6.1节](4.6.1.md)）。 其他媒体类型可以提供更细粒度的控制。

访问控制机制用于限制可以使用哪些`CRUD`操作。 特别是，`RESTCONF`与`NETCONF`访问控制模型（`NACM`）[[RFC6536](https://tools.ietf.org/html/rfc6536)]兼容，因为在`RESTCONF`和`NETCONF`操作之间存在特定映射。 资源路径需要由服务器在内部转换为相应的`YANG`实例标识。 使用此信息，服务器可以将`NACM`访问控制规则应用于`RESTCONF`消息。

服务器不得允许客户端无权访问的任何资源进行任何`RESTCONF`操作。

所有方法的实现（`PATCH` [[RFC5789](https://tools.ietf.org/html/rfc5789)]除外）在[[RFC7231](https://tools.ietf.org/html/rfc7231)]中定义。 本节定义每种`HTTP`方法的`RESTCONF`协议使用情况。
