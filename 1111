
**简要描述：**
- 功能： 返回新地址给商户平台
- 单次获取地址数量为N个（默认100，可调整），商户可根据实际需要请求多次。
- 针对EOS这类账户+memo模式的，这个接口只返回memo,配合接口：` $BaseURL/address/coinAccount `

**POST：**  ` $BaseURL/address/getBatch `


**参数列表：** 

|参数名|必选|类型|约束|说明|
|:-|:---|:----- |-----   |
|公共参数|是  |string |-- | 公共参数指：签名，版本、商户ID，时间。 |
|coin|是  |string |12个字符内主链币名| 币名HyperBC提供为准 |
|-|-|--|--|-----------------------------------|

## 关于合约币注意事项
- 针对合约币的地址获取特殊说明
合约币和主链币共享同一个地址，请只用主链币名进行申请即可，不支持用合约币名申请地址，对于商户平台同一个用户的一个或多个合约币及同属于一个主链的主链币，仅分配一个主链币地址即可。
案列：user_coin表

|用户ID|币名|地址|
|:----|:---| ---------------- |
|1688 |eth  |0xa6f8745c56a7c4fcb094678a2fbdcbd9ee9228f7  |
|1688 |usdt_erc20 |0xa6f8745c56a7c4fcb094678a2fbdcbd9ee9228f7  |
|1688 |leek  |0xa6f8745c56a7c4fcb094678a2fbdcbd9ee9228f7 |
|-|---|--------------------------------------------------|

- 注意：上面地址都属于ETH主链地址，同时也可以接收ETH合约币


**CURL完整请求案列**
```
curl http://api.test.hyperbc.com/shopapi/address/getBatch -H "Content-Type:application/json" -X POST -d '{
   "coin":"eth",
   "app_id":"hxgmau9imt86qky9",
   "version":"1.0",
   "time":1578997143,
"sign":"IUtWA3HEkK+wvTGaSBYwIrdx+ANyoOPl2/1LQTDevCSTxf4/lDXPrg6/ph+skNXIbZTR8Qs2yGGkqTUHEW/vbiTPzWkYZ874rRgplp06vhOBM/Pkw289K7PVCKy1ksOtLjwj1dUfDD/2AEqTgxRDjGyn+yDWRa7HLL/28bjU3pZoFwPPjbPyRxMK9BVL/li9IQ6hb8lyOyQNHNxS3C82sDVaQKqrB0dOqtP61OH0hBonrxMhBAMD8dUmaqO6Ef+bhHzbBm3BCC5VapkOkdthb+UWXKCiBoCipg3gqrwnBdOUGXqx/1mYicNZ+oHeVpBwnJlXudff6FT+HySszr5ISw=="
}'

说明：请求的URL可能每个对接商户不同，测试，正式环境也不同具体以对接约定为准

```



 **返回示例**

一、请求成功返回值
``` 
{
   "status": 200,
  "msg": "请求成功",
  "data": [
        "0x315898140acc2f8c1b7df8d61880d290289e3ebb",
        "0x854e1e685993aca23905a825344a417083c29dd3"
    ],
  "cachetime": "2020-01-09 15:48:42",
  "sign": "dGPAmtKvmXs5l4T6LPTzmwPKjArI76D2HyJdv9z3sduJgkWfUvpmcHJcjmxOoPzPz+D8KeoAOtCKXo8SiIEuFj74wce5r+Xad1kmyDLnuPYz4NVugqPWxxBVijbzgsieIiVpqMt3Q8pG0mQFr4TPf/QsDgOSkbhnHIyrxFGvKxo="
}
```


二、地址不足返回值
``` 
    {
      "status": 500,
      "msg": "地址不足",
      "data": null,
      "date_time": "2020-01-09 15:46:14",
      "sign": "rzbmkcf0Vr1AEZAo0Lsnlmk1s6HGONYZkpQxWKhGwIFxyN/fkaYzA6UxhIm9C8Drlfa8oZxpyrH89POuoaVfToxPhC9p8w10rfb4G/kNaZBE/gIo2H8e4/CTvEsiX5lz/ASNLiSe6BtHStUwMDCsl+ub7TF79uybb0RDy5mOegM="
    }
```

三、地址使用情况返回值
```
{
    "status":551,
    "msg":"有 6 个已分配未使用地址，请使用完再请求新的地址",
    "data":"6",
    "date_time":"2020-03-05 10:46:24",
    "time_stamp":1583376384,
    "sign":"e57nRfbDNvVIZuwvbXOsJaBnj9D+2hiP90SC8Q9ZCpdyTSbhB3WEpmotvZg11n3sW2Kzzle+ZSLPJH10iHqou3NgYzqEWD3EAThCzP0H8rhsj14NZ909JFAveRTe7XeP8xUcJINsY9HOliU2M5pt/qSnOx2CvdpFtxmVNLpIK+1VHdYuX6NRGc9TQ/Ptgwc6c9K7NNqqXY1y0e46LK8EBvXoEwbWa6L46f14Sx+/hN94Ymc6OKBUNFnbMGh31aeBp7E5YV/5fV2ZWKfNaNOxTyQVsPhpRt5NU9qCIzcgHKsqbroU72adWlBjyNrNWcXayilmwNHPAVJ1QKoqS6zoEQ=="
}
```

 **返回参数说明** 

|参数名|类型|约束|说明|
|:-----  |:-----|----- |----- |
|status |int | --  |状态码  |
|msg | string   | 100字内  |状态描述  |
|data | null或string或ObjectArray   | --  |返回数据主体  |
|date_time | DateTime   | --  |日期时间  |
|sign | string   | --  |返回签名  |

 **备注** 

- 更多返回错误代码请看首页的错误代码描述
