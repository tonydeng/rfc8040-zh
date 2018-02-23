# B.3.2. “`depth`”参数

“`depth`”参数用于限制服务器为`GET`方法请求返回的子资源的级别数。

“`depth`”参数在指定的目标资源级别开始计数级别，以便深度级别“`1`”仅包括目标资源级别本身。 深度级别“`2`”包括目标资源级别及其子节点。

此示例显示“`depth`”参数的不同值将如何影响用于检索顶层“`jukebox`”数据资源的回复内容。

示例1： `depth=unbounded`

要检索所有子资源，“`depth`”参数不存在或设置为默认值“`unbounded`”。

```HTTP
GET /restconf/data/example-jukebox:jukebox?depth=unbounded HTTP/1.1
Host: example.com
Accept: application/yang-data+json
```

服务器可能会如下回应：

```HTTP
HTTP/1.1 200 OK
Date: Thu, 26 Jan 2017 20:56:30 GMT
Server: example-server
Cache-Control: no-cache
Content-Type: application/yang-data+json

{
  "example-jukebox:jukebox" : {
    "library" : {
      "artist" : [
        {
          "name" : "Foo Fighters",
          "album" : [
            {
              "name" : "Wasting Light",
              "genre" : "example-jukebox:alternative",
              "year" : 2011,
              "song" : [
                {
                  "name" : "Wasting Light",
                  "location" :
                    "/media/foo/a7/wasting-light.mp3",
                  "format" : "MP3",
                  "length" : 286
                },
                {
                  "name" : "Rope",
                  "location" : "/media/foo/a7/rope.mp3",
                  "format" : "MP3",
                  "length" : 259
                }
              ]
            }
          ]
        }
      ]
    },
    "playlist" : [
      {
        "name" : "Foo-One",
        "description" : "example playlist 1",
        "song" : [
          {
            "index" : 1,
            "id" : "/example-jukebox:jukebox/library/artist[name='Foo Fighters']/album[name='Wasting Light']/song[name='Rope']"
          },
          {
            "index" : 2,
            "id" : "/example-jukebox:jukebox/library/artist[name='Foo Fighters']/album[name='Wasting Light']/song[name='Bridge Burning']"
          }
        ]
      }
    ],
    "player" : {
      "gap" : 0.5
    }
  }
}
```

示例2: `depth=1`

要确定给定目标资源是否存在一个或多个资源实例，请使用值“`1`”。

```HTTP
GET /restconf/data/example-jukebox:jukebox?depth=1 HTTP/1.1
Host: example.com
Accept: application/yang-data+json
```

服务器可能会如下回应：

```HTTP
HTTP/1.1 200 OK
Date: Thu, 26 Jan 2017 20:56:30 GMT
Server: example-server
Cache-Control: no-cache
Content-Type: application/yang-data+json

{
  "example-jukebox:jukebox" : {}
}
```

示例2: `depth=3`

将深度级别限制为目标资源加两个子级资源层，使用值“`3`”。

```HTTP
GET /restconf/data/example-jukebox:jukebox?depth=3 HTTP/1.1
Host: example.com
Accept: application/yang-data+json
```

服务器可能会如下回应：

```HTTP
HTTP/1.1 200 OK
Date: Thu, 26 Jan 2017 20:56:30 GMT
Server: example-server
Cache-Control: no-cache
Content-Type: application/yang-data+json

{
  "example-jukebox:jukebox" : {
    "library" : {
      "artist" : {}
    },
    "playlist" : [
      {
        "name" : "Foo-One",
        "description" : "example playlist 1",
        "song" : {}
      }
    ],
    "player" : {
      "gap" : 0.5
    }
  }
}
```
