##买卖盘实时成交数据
`目前支持人民币现货、美元现货`
###数据文件：
[BTC-CNY] `http://api.huobi.com/staticmarket/detail_btc_json.js`

[LTC-CNY] `http://api.huobi.com/staticmarket/detail_ltc_json.js`

[BTC-USD] `http://api.huobi.com/usdmarket/detail_btc_json.js`

###数据格式:(json)：
```javascript
{
  amount: 63165 //成交量
  level: 86.999 //涨幅
  buys: Array[10] //买10
  p_high: 4410 //最高
  p_last: 4275 //收盘价
  p_low: 4250 //最低
  p_new: 4362 //最新
  p_open: 4275 //开盘
  sells: Array[10] //卖10
  top_buy: Array[5] //买5
  top_sell: Array[5] //卖5 
  total: 273542407.24361 //总量（人民币） 
  trades: Array[15] //实时成交
  symbol:"btccny" //类型
}
```

买卖盘用例：

![买卖盘用例 ]( https://static.huobi.com/img/help/market_help_img3.png )

实时成交用例:

![实时成交用例 ]( https://static.huobi.com/img/help/market_help_img4.png )