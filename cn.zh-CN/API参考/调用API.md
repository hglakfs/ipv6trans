# 调用API {#concept_jyw_13k_qdb .concept}

IPv6转换服务接口调用是通过向IPv6转换服务API的服务端地址发送HTTP GET请求。您需要并按照接口说明在请求中加入相应请求参数，调用后系统会返回处理结果。请求及返回结果都使用UTF-8字符集进行编码。

## 请求结构 {#section_mqj_q3f_mdb .section}

IPv6转换服务的API是RPC风格，您可以通过发送HTTP GET请求调用IPv6转换服务API。

其请求结构如下：

```
http://Endpoint/?Action=xx&Parameters
```

其中：

-   Endpoint：IPv6转换服务API的服务接入地址为`vpc.aliyuncs.com`。
-   Action：要执行的操作，如使用DescribeIPv6Translators查询已创建的IPv6转换服务实例。
-   Version：要使用的API版本，IPv6转换服务的API版本是2016-04-28。
-   Parameters：请求参数，每个参数之间用“&”分隔。

    请求参数由公共请求参数和API自定义参数组成。公共参数中包含API版本号、身份验证等信息，详情参见。


下面是一个调用DescribeIPv6Translators接口查询已创建的IPv6转换服务实例的示例：

**说明：** 为了便于用户查看，本文档中的示例都做了格式化处理。

```
https://vpc.aliyuncs.com/?Action=DescribeIPv6Translators
&Format=xml
&Version=2016-04-28
&Signature=xxxx%xxxx%3D
&SignatureMethod=HMAC-SHA1
&SignatureNonce=15215528852396
&SignatureVersion=1.0
&AccessKeyId=key-test
&Timestamp=2012-06-01T12:00:00Z
…
```

## API授权 {#section_mlp_qmf_mdb .section}

为了确保您的账号安全，建议您使用子账号的身份凭证调用API。如果您使用RAM账号调用IPv6转换服务API，您需要为该RAM账号创建、附加相应的授权策略。

IPv6转换服务中可授权的资源和接口列表，参见[RAM鉴权](intl.zh-CN/API参考/RAM鉴权.md#)。

## API签名 {#section_jtc_ymf_mdb .section}

IPv6转换服务服务会对每个API请求进行身份验证，无论使用HTTP还是HTTPS协议提交请求，都需要在请求中包含签名（Signature）信息。

签名计算过程参见[RPC API签名](https://www.alibabacloud.com/help/doc-detail/66384.htm)。

IPv6转换服务通过使用AccessKey ID和AccessKey Secret进行对称加密的方法来验证请求的发送者身份。AccessKey是为阿里云账号和RAM用户发布的一种身份凭证\(类似于用户的登录密码\)，其中AccessKey ID 用于标识访问者的身份，AccessKey Secret是用于加密签名字符串和服务器端验证签名字符串的密钥，必须严格保密。

RPC API需按如下格式在请求中增加签名（Signature）：

`https://endpoint/?SignatureVersion=*1.0*&SignatureMethod=*HMAC-SHA1*&Signature=*CT9X0VtwR86fNWSnsc6v8YGOjuE%3D&SignatureNonce=3ee8c1b8-83d3-44af-a94f-4e0ad82fd6cf*`

以DescribeIPv6Translators为例，假设AccessKey ID是`testid`， AccessKey Secret是`testsecret`，则签名前的请求URL如下：

```
http://vpc.aliyuncs.com/?Action=DescribeIPv6Translators
&Timestamp=2016-02-23T12:46:24Z
&Format=XML
&AccessKeyId=testid
&SignatureMethod=HMAC-SHA1
&SignatureNonce=3ee8c1b8-83d3-44af-a94f-4e0ad82fd6cf
&Version=2014-05-26
&SignatureVersion=1.0
```

完成以下步骤计算签名：

1.  使用请求参数创建待签名字符串：

    ```
    GET&%2F&AccessKeyId%3Dtestid&Action%DescribeIPv6Translators&Format%3DXML&SignatureMethod%3DHMAC-SHA1&SignatureNonce%3D3ee8c1b8-83d3-44af-a94f-4e0ad82fd6cf&SignatureVersion%3D1.0&TimeStamp%3D2016-02-23T12%253A46%253A24Z&Version%3D2014-05-15
    ```

    。

2.  计算待签名的HMAC的值。

    在AccessKey Secret后添加一个“&”作为计算HMAC值的key。本示例中的key为`testsecret&`。

    ```
    CT9X0VtwR86fNWSnsc6v8YGOjuE=
    ```

3.  将签名加到请求参数中：

    ```
    http://vpc.aliyuncs.com/?Action=DescribeIPv6Translators
    &Timestamp=2016-02-23T12:46:24Z
    &Format=XML
    &AccessKeyId=testid
    &SignatureMethod=HMAC-SHA1
    &SignatureNonce=3ee8c1b8-83d3-44af-a94f-4e0ad82fd6cf
    &Version=2014-05-26
    &SignatureVersion=1.0
    &Signature=CT9X0VtwR86fNWSnsc6v8YGOjuE%3D
    ```


