# B.1.1. 检索顶级`API`资源

客户端通过检索`RESTCONF`根资源开始：

```HTTP
GET /.well-known/host-meta HTTP/1.1
Host: example.com
Accept: application/xrd+xml
```

服务器可能会如下回应：

```XML
HTTP/1.1 200 OK
Content-Type: application/xrd+xml
Content-Length: nnn

<XRD xmlns='http://docs.oasis-open.org/ns/xri/xrd-1.0'>
    <Link rel='restconf' href='/restconf'/>
</XRD>
```

客户端然后可以使用根资源“`/restconf`”来检索顶级`API`资源。

```HTTP
GET /restconf HTTP/1.1
Host: example.com
Accept: application/yang-data+json
```

服务器可能会如下回应：

```JSON
HTTP/1.1 200 OK
Date: Thu, 26 Jan 2017 20:56:30 GMT
Server: example-server
Content-Type: application/yang-data+json

{
  "ietf-restconf:restconf" : {
    "data" : {},
    "operations" : {},
    "yang-library-version" : "2016-06-21"
  }
}
```

如果要请求以`XML`格式编码响应内容，可以使用“`Accept`”头信息，如下面的示例请求所示：

```HTTP
GET /restconf HTTP/1.1
Host: example.com
Accept: application/yang-data+xml
```

服务器将以任何方式返回相同的概念数据，可能如下所示：

```XML
HTTP/1.1 200 OK
Date: Thu, 26 Jan 2017 20:56:30 GMT
Server: example-server
Cache-Control: no-cache
Content-Type: application/yang-data+xml

<restconf xmlns="urn:ietf:params:xml:ns:yang:ietf-restconf">
  <data/>
  <operations/>
  <yang-library-version>2016-06-21</yang-library-version>
</restconf>
```
