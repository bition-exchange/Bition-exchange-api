# Bition-exchange-api
## 1.目录
/open/api/all_order —— 获取全部委托

/open/api/all_trade —— 获取全部成交记录

/open/api/cancel_order —— 取消委托单

/open/api/common/symbols —— 查询系统支持的所有交易对及精度

/open/api/create_order —— 创建订单

/open/api/get_records —— 获取K线数据

/open/api/get_ticker —— 获取当前行情

/open/api/get_trades —— 获取行情成交记录

/open/api/market_dept —— 查询买卖盘深度

/open/api/market —— 获取各个币对的最新成交价

/open/api/new_order —— 获取当前委托

/open/api/order_info —— 获取订单详情

/open/api/user/account —— 资产余额
## 2.通用规则
签名：

请求参数按照字典排序，然后以keyvalue的形式拼接成字符串string，最后sign=MD5(string+secretKey)。注意：如果请求参数中value为NULL的情况，则在拼接字符串时不计入签名字符串。

例如：参数如下：
```
{

	country = 86;

	mobile = 15882133579;

	password = 654321zz;

	time = 1516007245;

}
```
 
拼接完成后：
```
string = country86mobile15882133579password654321zztime1516007278

sign=MD5(string+secretKey)
```
## 3.post请求参数采用表单格式提交数据
```
content-type:application/x-www-form-urlencoded
```

## 4.错误码
|错误码|说明|
|:---|:---|
|0|成功|
|5|下单失败|
|6|数量小于最小值|
|7|数量大于最小值|
|8|订单取消失败|
|9|交易被冻结|
|13|程序错误|
|19|余额不足|
|22|订单不存在|
|23|缺少交易数量参数|
|24|缺少交易价格参数|
|100001|系统异常|
|100002|系统升级|
|100004|请求参数不合法|
|100005|参数签名错误|
|100007|非法IP|
|110002|未知币种代号|

