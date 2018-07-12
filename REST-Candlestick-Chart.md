##实时行情数据接口
`目前支持人民币现货、美元现货`
###数据文件：
[BTC-CNY] `http://api.huobi.com/staticmarket/ticker_btc_json.js`

[LTC-CNY] `http://api.huobi.com/staticmarket/ticker_ltc_json.js`

[BTC-USD] `http://api.huobi.com/usdmarket/ticker_btc_json.js`

###数据格式:
```javascript
{"time":"1378137600","ticker":{"high":86.48,"low":79.75,"symbol":"btccny","last":83.9,"vol":2239560.1752883,"buy":83.88,"sell":83.9}}
```
报价：最高价，最低价，当前价，成交量，买1，卖1
##深度数据接口（json格式）
###数据文件
[BTC-CNY] `http://api.huobi.com/staticmarket/depth_btc_json.js`

[LTC-CNY] `http://api.huobi.com/staticmarket/depth_ltc_json.js`

[BTC-USD] `http://api.huobi.com/usdmarket/depth_btc_json.js`

指定深度数据条数（1-150条） 

[BTC-CNY] `http://api.huobi.com/staticmarket/depth_btc_X.js`

[LTC-CNY] `http://api.huobi.com/staticmarket/depth_ltc_X.js`

[BTC-USD] `http://api.huobi.com/usdmarket/depth_btc_X.js`

X表示返回多少条深度数据，可取值 1-150

###数据格式
```javascript
{"asks":[[90.8,0.5],...],"bids":[[86.06,79.243],...]],"symbol":"btccny"}
```

卖:价格:累积量,...    买:价格:累积量...

