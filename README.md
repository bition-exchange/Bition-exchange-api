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

## 5.地址
https://openapi.bition.pro/exchange-open-api

## 6.API
### 1) /open/api/all_order —— 获取全部委托(get)。包括已成交和已取消
|参数|填写类型|说明|
|:---|:---|:---|
|symbol|必填|市场标记，例如：ethbtc。见文档最后表一|
|pageSize|选填|页面大小|
|page|选填|页码|
|api_key|必填|api_key|
|time|必填|时间戳|
|sign|必填|签名|

返回

|字段|实例|说明|
|:---|:---|:---|
|code|0||
|msg|"suc"|code>0失败|
|data|如下||
```
{
	"count": 10,
	"orderList": [
		{
			"side": "BUY",
			"total_price": "0.10000000",
			"created_at": 1510993841000,
			"avg_price": "0.10000000",
			"countCoin": "btc",
			"source": 1,
			"type": 1,
			"side_msg": "买入",
			"volume": "1.000",
			"price": "0.10000000",
			"source_msg": "WEB",
			"status_msg": "完全成交",
			"deal_volume": "1.00000000",
			"id": 424,
			"remain_volume": "0.00000000",
			"baseCoin": "eth",
			"tradeList": [
				{
					"volume": "1.000",
					"feeCoin": "YLB",
					"price": "0.10000000",
					"fee": "0.16431104",
					"ctime": 1510996571195,
					"deal_price": "0.10000000",
					"id": 306,
					"type": "买入"
				}
			],
			"status": 2
		},
		{
			"side": "SELL",
			"total_price": "0.09900000",
			"created_at": 1510993715000,
			"avg_price": "0.10000000",
			"countCoin": "btc",
			"source": 1,
			"type": 1,
			"side_msg": "卖出",
			"volume": "1.000",
			"price": "0.09900000",
			"source_msg": "WEB",
			"status_msg": "完全成交",
			"deal_volume": "1.00000000",
			"id": 423,
			"remain_volume": "0.00000000",
			"baseCoin": "eth",
			"tradeList": [
				{
					"volume": "1.000",
					"feeCoin": "YLB",
					"price": "0.10000000",
					"fee": "0.16597075",
					"ctime": 1510993723973,
					"deal_price": "0.10000000",
					"id": 261,
					"type": "卖出"
				}
			],
			"status": 2
		}
	]
}
```
### 2) /open/api/all_trade 获取全部成交记录 (get)
|参数|填写类型|说明|
|:---|:---|:---|
|symbol|必填|市场标记，例如：ethbtc。见文档最后表一|
|pageSize|选填|页面大小|
|page|选填|页码|
|api_key|必填|api_key|
|time|必填|时间戳|
|sign|必填|签名|

返回

|字段|实例|说明|
|:---|:---|:---|
|code|0||
|msg|"suc"|code>0失败|
|data|如下||
```
{
	"count": 22,
	"resultList": [{
			"volume": "1.000",
			"side": "BUY",
			"feeCoin": "YLB",
			"price": "0.10000000",
			"fee": "0.16431104",
			"ctime": 1510996571195,
			"deal_price": "0.10000000",
			"id": 306,
			"type": "买入"
		},
		{
			"volume": "0.850",
			"side": "BUY",
			"feeCoin": "YLB",
			"price": "0.10000000",
			"fee": "0.13966438",
			"ctime": 1510996571190,
			"deal_price": "0.08500000",
			"id": 305,
			"type": "买入"
		},
		{
			"volume": "0.010",
			"side": "BUY",
			"feeCoin": "YLB",
			"price": "0.10000000",
			"fee": "0.00164311",
			"ctime": 1510995560344,
			"deal_price": "0.00100000",
			"id": 291,
			"type": "买入"
		},
		{
			"volume": "0.010",
			"side": "BUY",
			"feeCoin": "YLB",
			"price": "0.10000000",
			"fee": "0.00164311",
			"ctime": 1510995560338,
			"deal_price": "0.00100000",
			"id": 290,
			"type": "买入"
		},
		{
			"volume": "0.010",
			"side": "BUY",
			"feeCoin": "YLB",
			"price": "0.10000000",
			"fee": "0.00164311",
			"ctime": 1510995560331,
			"deal_price": "0.00100000",
			"id": 289,
			"type": "买入"
		},
		{
			"volume": "0.010",
			"side": "BUY",
			"feeCoin": "YLB",
			"price": "0.10000000",
			"fee": "0.00164311",
			"ctime": 1510995555323,
			"deal_price": "0.00100000",
			"id": 288,
			"type": "买入"
		},
		{
			"volume": "0.010",
			"side": "BUY",
			"feeCoin": "YLB",
			"price": "0.10000000",
			"fee": "0.00164311",
			"ctime": 1510995555317,
			"deal_price": "0.00100000",
			"id": 287,
			"type": "买入"
		},
		{
			"volume": "0.010",
			"side": "BUY",
			"feeCoin": "YLB",
			"price": "0.10000000",
			"fee": "0.00164311",
			"ctime": 1510995550309,
			"deal_price": "0.00100000",
			"id": 286,
			"type": "买入"
		},
		{
			"volume": "0.010",
			"side": "BUY",
			"feeCoin": "YLB",
			"price": "0.10000000",
			"fee": "0.00164311",
			"ctime": 1510995550303,
			"deal_price": "0.00100000",
			"id": 285,
			"type": "买入"
		},
		{
			"volume": "0.010",
			"side": "BUY",
			"feeCoin": "YLB",
			"price": "0.10000000",
			"fee": "0.00164311",
			"ctime": 1510995545295,
			"deal_price": "0.00100000",
			"id": 284,
			"type": "买入"
		}
	]
}
```
### 3) /open/api/cancel_order 取消委托单 (post)
|参数|填写类型|说明|
|:---|:---|:---|
|order_id|必填|订单ID|
|symbol|必填|市场标记，例如：ethbtc。见文档最后表一|
|api_key|必填|api_key|
|time|必填|时间戳|
|sign|必填|签名|

返回

|字段|实例|说明|
|:---|:---|:---|
|code|0||
|msg|"suc"|code>0失败|
|data|""||
