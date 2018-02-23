# B.2.1. 创建新的数据资源

要在“`libaray`”资源中创建新的“`artist`”资源，客户端可能会发送以下请求：

```HTTP
POST /restconf/data/example-jukebox:jukebox/library HTTP/1.1
Host: example.com
Content-Type: application/yang-data+json

{
  "example-jukebox:artist" : [
    {
      "name" : "Foo Fighters"
    }
  ]
}
```

如果资源已创建，则服务器可能会作出如下响应：

```HTTP
HTTP/1.1 201 Created
Date: Thu, 26 Jan 2017 20:56:30 GMT
Server: example-server
Location: https://example.com/restconf/data/example-jukebox:jukebox/library/artist=Foo%20Fighters
Last-Modified: Thu, 26 Jan 2017 20:56:30 GMT
ETag: "b3830f23a4c"
```

在“`jukebox`”中为该艺术家创建新的“`album`”资源资源，客户端可能会发送以下请求：

```HTTP
POST /restconf/data/example-jukebox:jukebox/library/artist=Foo%20Fighters HTTP/1.1
Host: example.com
Content-Type: application/yang-data+xml

<album xmlns="http://example.com/ns/example-jukebox">
  <name>Wasting Light</name>
  <year>2011</year>
</album>
```

如果资源已创建，则服务器可能会作出如下响应：

```HTTP
HTTP/1.1 201 Created
Date: Thu, 26 Jan 2017 20:56:30 GMT
Server: example-server
Location: https://example.com/restconf/data/example-jukebox:jukebox/library/artist=Foo%20Fighters/album=Wasting%20Light
Last-Modified: Thu, 26 Jan 2017 20:56:30 GMT
ETag: "b8389233a4c"
```
