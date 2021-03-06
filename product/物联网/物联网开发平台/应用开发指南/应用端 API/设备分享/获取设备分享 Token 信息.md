## 1. 接口描述

接口请求域名： `iot.cloud.tencent.com/api/exploreropen/tokenapi`。
本接口（AppDescribeShareDeviceToken）用于获取设备分享 Token 信息。

## 2. 输入参数

| 名称             | 类型   | 必选 | 描述                                                         |
| ---------------- | ------ | ---- | ------------------------------------------------------------ |
| AccessToken      | String | 是   | 公共参数，AccessToken 用于对一个已经登录的用户鉴权。         |
| RequestId        | String | 是   | 公共参数，唯一请求 ID，可自行生成，推荐使用 uuId。定位问题时，需提供该次请求的 RequestId。 |
| Action           | String | 是   | 公共参数，本接口取值：AppDescribeShareDeviceToken。            |
| ShareDeviceToken | String | 是   | 设备分享 Token。                                                |

## 3. 输出参数

| 名称                 | 类型                                                         | 描述                                                         |
| -------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| RequestId            | String                                                       | 公共参数，唯一请求ID，与入参相同，定位问题时，需提供该次请求的 RequestId。 |
| ShareDeviceTokenInfo | Object of [ShareDeviceTokenInfo](https://cloud.tencent.com/document/product/1081/40780#sharedevicetokeninfo) | 响应的结果。                    |

## 4. 示例
**输入示例**

```HTTP
POST https://iot.cloud.tencent.com/api/exploreropen/tokenapi HTTP/1.1
content-type: application/json
{
  "Action": "AppDescribeShareDeviceToken",
  "AccessToken": "8b4a70dd16105f******************18edd4e78a3bb8ec",
  "RequestId": "1555507****15",
  "ShareDeviceToken": "49d2b71dc5814354****8a4c756d3ce9"
}
```

**输出示例:  成功**

```json
// UserId、UserNick 在被分享者接受前为空
// 被分享者接受分享后，UserId 保存的是被分享者的信息
// 前端可以通过UserId是否为空，来判断绑定情况。
{
  "Response": {
    "RequestId": "1555507****15",
    "ShareDeviceTokenInfo": {
      "FromUserId": "1",
      "FromUserNick": "tests",
      "UserId": "2",
      "UserNick": "test2",
      "ProductId": "22F9Y6II7O",
      "DeviceName": "light1",
      "AliasName": "my_light",
      "IconUrl": "",
      "BindTime": 0,
      "ExpireTime": 1574757262,
      "CreateTime": 1574152462
    }
  }
}
```

**输出示例:  失败**

```json
{
  "Response": {
    "Error": {
      "Code": "InvalidParameterValue.InvalidShareDeviceToken",
      "Message": "设备分享Token无效"
    },
    "RequestId": "1555507****15"
  }
}
```


## 5. 错误码

| 错误码                                        | 描述              |
| --------------------------------------------- | ----------------- |
| InternalError                                 | 内部错误。          |
| InvalidParameterValue                         | 参数取值错误。      |
| InvalidParameterValue.InvalidShareDeviceToken | 设备分享 Token 无效。 |

