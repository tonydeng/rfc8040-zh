# B.2.5. 编辑数据资源

在本例中，客户端通过发送数据资源的`PATCH`添加“`album`”子资源来修改一个数据节点：

```XML
PATCH /restconf/data/example-jukebox:jukebox/library/artist=Nick%20Cave%20and%20the%20Bad%20Seeds HTTP/1.1
Host: example.com
Content-Type: application/yang-data+xml

<artist xmlns="http://example.com/ns/example-jukebox">
  <name>Nick Cave and the Bad Seeds</name>
  <album>
    <name>The Good Son</name>
    <year>1990</year>
  </album>
</artist>
```
