# B.3.3. “`fields`”参数

在本例中，客户端正在以`JSON`格式检索数据存储资源，但仅检索“`modules-state/module`”列表，并且仅检索每个列表条目中的“`name`”和“`revision`”节点。 请注意，服务器返回的顶层节点与目标资源节点（本例中为“`data`”）匹配。 “`module-set-id`”叶子没有被返回，因为它没有在`fields`表达式中被选中。

```HTTP
GET /restconf/data?fields=ietf-yang-library:modules-state/module(name;revision) HTTP/1.1
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
  "ietf-restconf:data" : {
    "ietf-yang-library:modules-state" : {
      "module" : [
        {
          "name" : "example-jukebox",
          "revision" : "2016-08-15"
        },
        {
          "name" : "ietf-inet-types",
          "revision" : "2013-07-15"
        },
        {
          "name" : "ietf-restconf-monitoring",
          "revision" : "2017-01-26"
        },
        {
          "name" : "ietf-yang-library",
          "revision" : "2016-06-21"
        },
        {
          "name" : "ietf-yang-types",
          "revision" : "2013-07-15"
        }
      ]
    }
  }
}
```
