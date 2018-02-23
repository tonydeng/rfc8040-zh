# B.3.9. “`with-defaults`”参数

假设服务器实现[[RFC6243](https://tools.ietf.org/html/rfc6243)]的[附录A.1](https://tools.ietf.org/html/rfc6243#appendix-A.1)中定义的模块“`example`”，并且假定服务器的数据存储如[[RFC6243](https://tools.ietf.org/html/rfc6243)]的[附录A.2](https://tools.ietf.org/html/rfc6243#appendix-A.2)中所定义。

如果服务器的“`defaults`”协议能力`URI`（[第9.1.2节](../section-9/9.1.2.md)）中的“`basic-mode`”参数是“`trim`”，则接口“`eth1`”的以下请求可能如下所示：

没有查询参数：

```HTTP
GET /restconf/data/example:interfaces/interface=eth1 HTTP/1.1
Host: example.com
Accept: application/yang-data+json
```

服务器可能会如下回应：

```HTTP
HTTP/1.1 200 OK
Date: Thu, 26 Jan 2017 20:56:30 GMT
Server: example-server
Content-Type: application/yang-data+json

{
  "example:interface" : [
    {
      "name" : "eth1",
      "status" : "up"
    }
  ]
}
```

请注意，缺少“`mtu`”叶字节点，因为它被设置为默认“`1500`”，并且服务器的默认处理“`basic-mode`”参数是“`trim`”。

使用查询参数：

```HTTP
GET /restconf/data/example:interfaces/interface=eth1?with-defaults=report-all HTTP/1.1
Host: example.com
Accept: application/yang-data+json
```

服务器可能会如下回应：

```HTTP
HTTP/1.1 200 OK
Date: Thu, 26 Jan 2017 20:56:30 GMT
Server: example-server
Content-Type: application/yang-data+json

{
  "example:interface" : [
    {
      "name" : "eth1",
      "mtu" : 1500,
      "status" : "up"
    }
  ]
}
```

请注意，服务器返回“`mtu`”叶子节点，因为“`report-all`”使用“`with-defaults`”查询参数请求模式。
