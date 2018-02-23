# 附录A. 示例`YANG`模块

本文档中使用的示例`YANG`模块代表一个简单的媒体点播机界面。

“`example-jukebox`”模块的`YANG`树图：

```
+--rw jukebox!
   +--rw library
   |  +--rw artist* [name]
   |  |  +--rw name     string
   |  |  +--rw album* [name]
   |  |     +--rw name     string
   |  |     +--rw genre?   identityref
   |  |     +--rw year?    uint16
   |  |     +--rw admin
   |  |     |  +--rw label?              string
   |  |     |  +--rw catalogue-number?   string
   |  |     +--rw song* [name]
   |  |        +--rw name        string
   |  |        +--rw location    string
   |  |        +--rw format?     string
   |  |        +--rw length?     uint32
   |  +--ro artist-count?   uint32
   |  +--ro album-count?    uint32
   |  +--ro song-count?     uint32
   +--rw playlist* [name]
   |  +--rw name           string
   |  +--rw description?   string
   |  +--rw song* [index]
   |     +--rw index    uint32
   |     +--rw id       instance-identifier
   +--rw player
      +--rw gap?   decimal64
```

rpcs:

```
+---x play
   +--ro input
      +--ro playlist       string
      +--ro song-number    uint32
```
