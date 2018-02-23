# B.3.5. “`point`”参数

在这个例子中，客户在第一首歌曲后在“`Foo-One`”播放列表中插入新的歌曲条目。

客户端请求：

```HTTP
POST /restconf/data/example-jukebox:jukebox/\
    playlist=Foo-One?insert=after&point=\
    %2Fexample-jukebox%3Ajukebox\
    %2Fplaylist%3DFoo-One%2Fsong%3D1 HTTP/1.1
Host: example.com
Content-Type: application/yang-data+json

{
  "example-jukebox:song" : [
     {
       "index" : 2,
       "id" : "/example-jukebox:jukebox/library/artist[name='Foo Fighters']/album[name='Wasting Light']/song[name='Bridge Burning']"
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
Location: https://example.com/restconf/data/example-jukebox:jukebox/playlist=Foo-One/song=2
ETag: "abcada438af"
mi
```
