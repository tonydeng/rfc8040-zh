# B.2.4. 替换数据存储资源

在这个例子中，整个配置数据存储内容正在被替换。 任何未出现在`<data>`元素中但存在于服务器中的子节点都将被删除。

```XML
PUT /restconf/data HTTP/1.1
Host: example.com
Content-Type: application/yang-data+xml

<data xmlns="urn:ietf:params:xml:ns:yang:ietf-restconf">
  <jukebox xmlns="http://example.com/ns/example-jukebox">
    <library>
      <artist>
        <name>Foo Fighters</name>
        <album>
          <name>One by One</name>
          <year>2012</year>
        </album>
      </artist>
      <artist>
        <name>Nick Cave and the Bad Seeds</name>
        <album>
          <name>Tender Prey</name>
          <year>1988</year>
        </album>
      </artist>
    </library>
  </jukebox>
</data>
```
