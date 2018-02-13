# 7. 错误报告

`HTTP`状态代码用于报告`RESTCONF`操作的成功或失败。 `NETCONF`错误响应包含在`<rpc-error>`元素中的错误信息适用于`RESTCONF`，并且为“`4xx`”和“`5xx`”类状态码返回`<errors>`数据树信息。

由于操作资源是使用`YANG`的“`rpc`”语句来定义，而操作是使用`YANG`的“`action`”语句来定义，因此需要将`NETCONF`的`<error-tag>`值映射到`HTTP`状态代码。 要使用的特定错误标记和响应代码特定于数据模型，并且可能包含在“`action`”或“`rpc`”语句的`YANG`的“`description`”语句中。

#### 从`<errot-tag>`映射到`HTTP`状态码

| error-tag | status code |
| :------------- | :------------- |
| in-use                  | 409              |
| invalid-value           | 400, 404, or 406 |
| (request) too-big       | 413              |
| (response) too-big      | 400              |
| missing-attribute       | 400              |
| bad-attribute           | 400              |
| unknown-attribute       | 400              |
| bad-element             | 400              |
| unknown-element         | 400              |
| unknown-namespace       | 400              |
| access-denied           | 401 or 403       |
| lock-denied             | 409              |
| resource-denied         | 409              |
| rollback-failed         | 500              |
| data-exists             | 409              |
| data-missing            | 409              |
| operation-not-supported | 405 or 501       |
| operation-failed        | 412 or 500       |
| partial-operation       | 500              |
| malformed-message       | 400              |
