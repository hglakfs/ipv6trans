# RAM鉴权 {#reference_ow1_hkk_qdb .reference}

在使用RAM账号调用IPv6转换服务前API前，需要主账号通过创建授权策略对RAM账号进行授权。在授权策略中，使用资源描述符（Alibaba Cloud Resource Name, ARN）指定授权资源。

下表列举了IPv6转换服务可授权的API及其描述方式：

-   `"acs:vpc:$regionid:$accountid:ipv6trans/*`
-   `"acs:vpc:$regionid:$accountid:ipv6trans/$ipv6transid`
-   `"acs:vpc:$regionid:$accountid:ipv6trans/$ipv6transentryid`
-   `acs":vpc::$accountid:ipv6trans/`

    其中`$regionid/accoutid/vrouterid...` 为具体的资源ID，`*`代表对应的所有资源。


