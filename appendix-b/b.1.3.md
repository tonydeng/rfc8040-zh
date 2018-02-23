# B.1.3. 检索服务器功能信息

在本例中，客户端以`XML`格式从服务器获取能力信息，服务器支持所有`RESTCONF`查询参数以及一个供应商参数：

```HTTP
GET /restconf/data/ietf-restconf-monitoring:restconf-state/capabilities HTTP/1.1
Host: example.com
Accept: application/yang-data+xml
```

服务器可能会如下回应：

```XML
HTTP/1.1 200 OK
Date: Thu, 26 Jan 2017 20:56:30 GMT
Server: example-server
Cache-Control: no-cache
Last-Modified: Thu, 26 Jan 2017 16:00:14 GMT
Content-Type: application/yang-data+xml

<capabilities
    xmlns="urn:ietf:params:xml:ns:yang:ietf-restconf-monitoring">
 <capability>urn:ietf:params:restconf:capability:defaults:1.0?basic-mode=explicit</capability>
 <capability>urn:ietf:params:restconf:capability:with-defaults:1.0</capability>
 <capability>urn:ietf:params:restconf:capability:depth:1.0</capability>
 <capability>urn:ietf:params:restconf:capability:fields:1.0</capability>
 <capability>urn:ietf:params:restconf:capability:filter:1.0</capability>
 <capability>urn:ietf:params:restconf:capability:start-time:1.0</capability>
 <capability>urn:ietf:params:restconf:capability:stop-time:1.0</capability>
 <capability>http://example.com/capabilities/myparam</capability>
</capabilities>
```
