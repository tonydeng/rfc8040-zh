# B.3.4. “`insert`”参数

在这个例子中，“`Foo-One`”播放列表中新的第一首歌曲正在创建。

客户端请求：

```HTTP
POST /restconf/data/example-jukebox:jukebox/playlist=Foo-One?insert=first HTTP/1.1
Host: example.com
Content-Type: application/yang-data+json

{
  "example-jukebox:song" : [
     {
       "index" : 1,
       "id" : "/example-jukebox:jukebox/library/artist[name='Foo Fighters']/album[name='Wasting Light']/song[name='Rope']"
     }
   ]
}
```

服务器响应：

```HTTP
HTTP/1.1 201 Created
Date: Thu, 26 Jan 2017 20:56:30 GMT
Server: example-server
Last-Modified: Thu, 26 Jan 2017 20:56:30 GMT
Location: https://example.com/restconf/data/example-jukebox:jukebox/playlist=Foo-One/song=1
ETag: "eeeada438af"
```
