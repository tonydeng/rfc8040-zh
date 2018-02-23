# B.2.3. 编辑数据存储资源

在此示例中，假定示例系统模块中有一个名为“`system`”的顶级数据资源，并且此容器具有名为“`enable-jukebox-streaming`”的子叶节点：

```YANG
container system {
  leaf enable-jukebox-streaming {
    type boolean;
  }
}
```

在此示例中，客户端使用`PATCH`一次修改两个顶级资源，以启用点播机流并为两个“`artist`”资源中的每一个添加“`album`”子资源：

```XML
PATCH /restconf/data HTTP/1.1
Host: example.com
Content-Type: application/yang-data+xml

<data xmlns="urn:ietf:params:xml:ns:yang:ietf-restconf">
  <system xmlns="http://example.com/ns/example-system">
    <enable-jukebox-streaming>true</enable-jukebox-streaming>
  </system>
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
