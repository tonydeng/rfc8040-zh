# B.3.1. “`content`”参数

“`content`”参数用于选择服务器为`GET`方法请求返回的数据子资源类型（配置和/或非配置）。

在这个例子中，使用了一个简单的`YANG`列表，它具有配置和非配置子资源。

```YANG
container events {
  list event {
    key name;
    leaf name { type string; }
    leaf description { type string; }
    leaf event-count {
      type uint32;
      config false;
    }
  }
}
```

示例1：`content=all`

要检索所有子资源，可以将“`content`”参数设置为“`all`”，因为这是默认值，或可以省略该参数。 客户端可能会发送以下内容：

```HTTP
GET /restconf/data/example-events:events?content=all HTTP/1.1
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
  "example-events:events" : {
    "event" : [
      {
        "name" : "interface-up",
        "description" : "Interface up notification count",
        "event-count" : 42
      },
      {
        "name" : "interface-down",
        "description" : "Interface down notification count",
        "event-count" : 4
      }
    ]
  }
}
```

示例2：`content=config`

要仅检索配置子资源，“`content`”参数设置为“`config`”。 请注意，只有“`content`”参数值为“`config`”时，才会返回“`ETag`”和“`Last-Modified`”标题。


```HTTP
GET /restconf/data/example-events:events?content=config HTTP/1.1
Host: example.com
Accept: application/yang-data+json
```

服务器可能会如下回应：

```HTTP
HTTP/1.1 200 OK
Date: Thu, 26 Jan 2017 20:56:30 GMT
Server: example-server
Last-Modified: Thu, 26 Jan 2017 16:45:20 GMT
ETag: "eeeada438af"
Cache-Control: no-cache
Content-Type: application/yang-data+json

{
  "example-events:events" : {
    "event" : [
      {
        "name" : "interface-up",
        "description" : "Interface up notification count"
      },
      {
        "name" : "interface-down",
        "description" : "Interface down notification count"
      }
    ]
  }
}
```

示例2：`content=nonconfig`

要仅检索非配置子资源，“`content`”参数设置为“`nonconfig`”。 请注意，还会返回配置祖先（如果有）和列表键叶（如果有）。 客户端可能会发送以下内容：

```HTTP
GET /restconf/data/example-events:events?content=nonconfig HTTP/1.1
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
  "example-events:events" : {
    "event" : [
      {
        "name" : "interface-up",
        "event-count" : 42
      },
      {
        "name" : "interface-down",
        "event-count" : 4
      }
    ]
  }
}
```
