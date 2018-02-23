# B.1.2. 检索服务器模块信息

`YANG`模块库可能随时间而改变。 如前一节所述，客户端可以从`API`资源中检索服务器支持的“`ietf-yang-library`”模块的修订日期。

在本例中，客户端以`JSON`格式从服务器中检索模块信息：

```HTTP
GET /restconf/data/ietf-yang-library:modules-state HTTP/1.1
Host: example.com
Accept: application/yang-data+json
```

服务器可能会如下回应：

```JSON
HTTP/1.1 200 OK
Date: Thu, 26 Jan 2017 20:56:30 GMT
Server: example-server
Cache-Control: no-cache
Last-Modified: Thu, 26 Jan 2017 14:00:14 GMT
Content-Type: application/yang-data+json

{
  "ietf-yang-library:modules-state" : {
    "module-set-id" : "5479120c17a619545ea6aff7aa19838b036ebbd7",
    "module" : [
      {
        "name" : "foo",
        "revision" : "2012-01-02",
        "schema" : "https://example.com/modules/foo/2012-01-02",
        "namespace" : "http://example.com/ns/foo",
        "feature" : [ "feature1", "feature2" ],
        "deviation" : [
          {
            "name" : "foo-dev",
            "revision" : "2012-02-16"
          }
        ],
        "conformance-type" : "implement"
      },
      {
        "name" : "ietf-yang-library",
        "revision" : "2016-06-21",
        "schema" : "https://example.com/modules/\
          ietf-yang-library/2016-06-21",
        "namespace" :
          "urn:ietf:params:xml:ns:yang:ietf-yang-library",
        "conformance-type" : "implement"
      },
      {
        "name" : "foo-types",
        "revision" : "2012-01-05",
        "schema" :
          "https://example.com/modules/foo-types/2012-01-05",
        "namespace" : "http://example.com/ns/foo-types",
        "conformance-type" : "import"
      },
      {
        "name" : "bar",
        "revision" : "2012-11-05",
        "schema" : "https://example.com/modules/bar/2012-11-05",
        "namespace" : "http://example.com/ns/bar",
        "feature" : [ "bar-ext" ],
        "conformance-type" : "implement",
        "submodule" : [
          {
            "name" : "bar-submod1",
            "revision" : "2012-11-05",
            "schema" :
             "https://example.com/modules/bar-submod1/2012-11-05"
          },
          {
            "name" : "bar-submod2",
            "revision" : "2012-11-05",
            "schema" :
             "https://example.com/modules/bar-submod2/2012-11-05"
          }
        ]
      }
    ]
  }
}
```
