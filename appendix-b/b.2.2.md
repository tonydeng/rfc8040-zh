# B.2.2. 检测数据存储资源实体-标签更改

在此示例中，服务器仅支持数据存储区上次更改的时间戳。 假设客户端缓存了对前一个请求的响应中的“`Last-Modified`”头信息。 该值用于以下请求中的“`If-Unmodified-Since`”头信息中，以用键值“`Wasting Light`”修补“`album`”列表条目。 只有“`genre`”字段正在更新。

```HTTP
PATCH /restconf/data/example-jukebox:jukebox/library/artist=Foo%20Fighters/album=Wasting%20Light/genre HTTP/1.1
Host: example.com
If-Unmodified-Since: Thu, 26 Jan 2017 20:56:30 GMT
Content-Type: application/yang-data+json

{ "example-jukebox:genre" : "example-jukebox:alternative" }
```

在此示例中，数据存储区资源自“`If-Unmodified-Since`”标题中指定的时间以来已更改。 服务器可能会如下回应：

```HTTP
HTTP/1.1 412 Precondition Failed
Date: Thu, 26 Jan 2017 20:56:30 GMT
Server: example-server
Last-Modified: Thu, 26 Jan 2017 19:41:00 GMT
ETag: "b34aed893a4c"
```
