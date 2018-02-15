# 9. RESTCONF监测

“`ietf-restconf-monitoring`”的模块提供有关服务器可用的`RESTCONF`协议功能和事件流的信息。 `RESTCONF`服务器必须执行“`ietf-restconf-monitoring`”的模块。

用于“`ietf-restconf-monitoring`”模块的`YANG`树图：

```
+--ro restconf-state
   +--ro capabilities
   |  +--ro capability*   inet:uri
   +--ro streams
      +--ro stream* [name]
         +--ro name                        string
         +--ro description?                string
         +--ro replay-support?             boolean
         +--ro replay-log-creation-time?   yang:date-and-time
         +--ro access* [encoding]
            +--ro encoding  string
            +--ro location  inet:uri
```
