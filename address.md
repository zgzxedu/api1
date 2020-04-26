    
**简要描述：** 
- 商户将地址分配给用户后，一定要通过“状态同步接口”通知HyperBC进行地址使用状态更新。

**POST：**   ` $BaseUrl/address/syncStatus `

**参数：** 

|参数名|必选|类型|约束|说明|
|:-|-|:--|----|-------------------|
|公共参数 |是  |string |--| 公参指：签名，版本、商户ID，时间|
|address  |是  |string |128个字符以内 | 地址  |
|coin |是  |string | 12个字符以内 | 地址所属主链币种    |
|user_id |是  |string | 2^31以内数值字符串| 地址分配给了那个用户的UID    |
|--|--|-- |--|-------------------------------------|

参数提交格式：JSON格式

**CURL请求案列：**

```
curl http://api.test.hyperbc.com/shopapi/address/syncStatus -H "Content-Type:application/json" -X POST -d '{
    "app_id":"hxgmau9imt86qky9",
    "version":"1.0",
    "time":1579002849,
    "address":"0x0603b5a606e6ae28e729d145f4d5a99bd8769950",
    "coin":"eth",
    "user_id":"3",
"sign":"oilW6DAWpBSDssoGFkIvW/GRTIt4NWEc92P2L/G/+S3YvbKJxpZRvRc/Tjb3iLX4C/LDGs2ZWcKPDoIbq2BqYKS1EWMfDIjCI/tbuK7gPwOr50sPeyDoldUx8ZZXZ0TARqJLRz90rm2hYO0NOjxczC9ECI1twgcCQT9grHIaiwBDVeVU8QfQ7OfQ4MXPMO2CkYSa+sqsyEbqcuIzvsq6yg6JPMjUqdGTb8rObuL0kXt511ZgpK6cxBgIUnOVmvJX25FuvwTEeBlmQrxgrtUUQ5KzG3UvCy9GZHyDU0E+BJGA2X6S6cmbWSs74MpGUo3l+E8zcLYAUkTed0NSFWOLpA=="
}'

```

 **成功响应结果：**

``` 
{
    "status":200,
    "msg":"同步成功",
    "data":{
        "address":"0x0603b5a606e6ae28e729d145f4d5a99bd8769950",
        "coin":"eth"
    },
	"date_time":"2020-01-14 00:33:58",  	     "sign":"KVZrYNjK9xwZvqJHMSRxxK4PjbirEtS1vyI220BzK/rF7bp+iU+ClQU5BSERcaujFz0EqRtZW5LSojjgRPeGbh4Wyqmlpk/Qz7ulTC0lqkik3torj3xL4SP2MKvUMXyPRRn8MKh586c8XLF1APRR48mdlDVQgxdUmr9mtB8ssLI="
}

```

 **异常返回示例**

``` 
{
    "status":565,
    "msg":"该币种不支持",
    "data":null,
    "date_time":"2020-03-05 11:15:44",
    "time_stamp":1583378144,
    "sign":"lZOEG+O2jhDIZd9vQnvQl32kj10F0nN4dHPK7FwPm73lALkEiM3boAo++WTIFtrzLno8117QpoUpIHax7Lqh8ECeit+O7+1S8Ri0buLuBA1Rm/W98SY9gbGu4PFTJn4sMBhO/FyZ6zB36vUiJhnbNMtS0u/ePqNXzhWyJZpZIUEs7ESz8MJJMb55bIdZjp+wGnEiYVYJhX0d2XRywtZ3037ZaniobIaTqQrdAW8tZDuIXTo5GOKgSGWTzBH6T194iqmb2opj6nihlCn/6MHtfqGNbv3tn6J+JD63xQ+w5r4NVmr4MD7+jBL+IkXXyk07TgqBcNuL2XqH39AVzkweVQ=="
}

```

 **返回参数说明** 

|参数名|必选|类型|约束|说明|
|:----    |:---|:----- |-----   |
|status |是  |int | -- |返回状态码   |
|msg | 是  |string | --| 状态码描述   |
|date_time | 是  |string |--| 接口返回时间   |
|time_stamp | 是  |string |--| 无时区时间单位秒   |
|data |是  |null或JSONObjectString |-- | 返回数据    |
|sign |是  |string | -- | 后端签名    |



## 安全注意事项
注意：商户把地址分配给自己的用户后，一定要请求该接口回传使用状态信息，并获取到 200正确状态码返回值后再开启用户的充提现功能。

1、如果不同步会影响地址获取接口的使用（已分配未使用的地址数量 超过一定量时，HyperBC不再分配新的地址给商家）。

2、如果状态同步没有收到正确返回结果，而是报错提示，请人工排查错误。
设计规则：相同币种或合约币，相同商家，相同用户ID 只能分配一个地址。
如果违法上面规则会报错。

 **备注** 

- 更多返回错误代码请看首页的错误代码描述

 
