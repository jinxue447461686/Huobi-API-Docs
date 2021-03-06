# WebSocket API Reference

## 订阅 KLine 数据 market.$symbol.kline.$period

成功建立和 WebSocket API 的连接之后，向 Server 发送如下格式的数据来订阅数据：
```
{
  "sub": "market.$symbol.kline.$period",
  "id": "id generate by client"
}
```

| 参数名称         | 是否必须  | 类型     | 描述                | 默认值   | 取值范围                                     |
| ------------ | ----- | ------ | ----------------- | ----- | ---------------------------------------- |
| symbol       | true  | string | 交易对                |       | ethbtc, ltcbtc, etcbtc, bchbtc......以下新的symbol会在生效日当天可以请求：huobi10 - 指数，hb10 - ETF净值 |
| period       | true  | string | K线周期          |       | 1min, 5min, 15min, 30min, 60min, 1day, 1mon, 1week, 1year |

**正确订阅的例子**

正确订阅
```
{
  "sub": "market.btcusdt.kline.1min",
  "id": "id1"
}
```

订阅成功返回数据的例子
```
{
  "id": "id1",
  "status": "ok",
  "subbed": "market.btcusdt.kline.1min",
  "ts": 1489474081631
}
```

之后每当 KLine 有更新时，client 会收到数据，例子
```
{
  "ch": "market.btcusdt.kline.1min",
  "ts": 1489474082831,
  "tick": {
    "id": 1489464480,
    "amount": 0.0,
    "count": 0,
    "open": 7962.62,
    "close": 7962.62,
    "low": 7962.62,
    "high": 7962.62,
    "vol": 0.0
  }
}
```

tick 说明
```
  "tick": {
    "id": K线id,
    "amount": 成交量,
    "count": 成交笔数,
    "open": 开盘价,
    "close": 收盘价,当K线为最晚的一根时，是最新成交价
    "low": 最低价,
    "high": 最高价,
    "vol": 成交额, 即 sum(每一笔成交价 * 该笔的成交量)
  }

```

**错误订阅的例子**

错误订阅(错误的 symbol)
```
{
  "sub": "market.invalidsymbol.kline.1min",
  "id": "id2"
}
```

订阅失败返回数据的例子
```
{
  "id": "id2",
  "status": "error",
  "err-code": "bad-request",
  "err-msg": "invalid topic market.invalidsymbol.kline.1min",
  "ts": 1494301904959
}
```

错误订阅(错误的 topic)
```
{
  "sub": "market.btcusdt.kline.3min",
  "id": "id3"
}
```

订阅失败返回数据的例子
```
{
  "id": "id3",
  "status": "error",
  "err-code": "bad-request",
  "err-msg": "invalid topic market.btcusdt.kline.3min",
  "ts": 1494310283622
}
```

## 请求 KLine 数据 market.$symbol.kline.$period  

```
{
  "req": "market.$symbol.kline.$period",
  "id": "id generated by client",
  "from": "optional, type: long, 2017-07-28T00:00:00+08:00 至 2050-01-01T00:00:00+08:00 之间的时间点，单位：秒",
  "to": "optional, type: long, 2017-07-28T00:00:00+08:00 至 2050-01-01T00:00:00+08:00 之间的时间点，单位：秒，必须比 from 大"
}
```

| 参数名称         | 是否必须  | 类型     | 描述                | 默认值   | 取值范围                                     |
| ------------ | ----- | ------ | ----------------- | ----- | ---------------------------------------- |
| symbol       | true  | string | 交易对                |       | btcusdt, ethusdt, ltcusdt, etcusdt, bchusdt, ethbtc, ltcbtc, etcbtc, bchbtc... 以下新的symbol会在生效日当天可以请求：huobi10 - 指数，hb10 - ETF净值|
| period       | true  | string | K线周期          |       | 1min, 5min, 15min, 30min, 60min, 1day, 1mon, 1week, 1year |

##### 关于ETF请求参数的说明

Symbol|说明
--|--|
huobi1o|指数|
hb20| ETF净值|

其他请求参数`period`,`from`,`to`保持不变。

* 响应结果

响应结果的结构保持不变，唯一的区别是响应结果中的amount, count 和 vol都是0，因为在这里的amount, count 和 vol是交易的相关的 值，而指数和ETF净值没有相应的数据。Houbi10 指数和 Hb10净值每15秒更新一次。 

`[t1, t5]`
假设有 t1 ~ t5 的K线.

* from: t1, to: t5, return [t1, t5].
* from: t5, to: t1, which t5 > t1, return [].
* from: t5, return [t5].
* from: t3, return [t3, t5].
* to: t5, return [t1, t5].
* from: t which t3 < t <t4, return [t4, t5].
* to: t which t3 < t <t4, return [t1, t3].
* from: t1 and to: t2, should satisfy 1501171200 < t1 < t2 < 2524579200.

```
一次最多300条
```

#### 请求 KLine 数据的例子

```
{
  "req": "market.btcusdt.kline.1min",
  "id": "id10"
}
```

返回数据的例子
```
{
  "rep": "market.btcusdt.kline.1min",
  "status": "ok",
  "id": "id10",
  "tick": [
    {
      "amount": 17.4805,
      "count":  27,
      "id":     1494478080,
      "open":   10050.00,
      "close":  10058.00,
      "low":    10050.00,
      "high":   10058.00,
      "vol":    175798.757708
    },
    {
      "amount": 15.7389,
      "count":  28,
      "id":     1494478140,
      "open":   10058.00,
      "close":  10060.00,
      "low":    10056.00,
      "high":   10065.00,
      "vol":    158331.348600
    },
    // more KLine data here
  ]
}
```

## 订阅 Market Depth 数据 market.$symbol.depth.$type 

成功建立和 WebSocket API 的连接之后，向 Server 发送如下格式的数据来订阅数据：
```
{
  "sub": "market.$symbol.depth.$type",
  "id": "id generated by client"
}
```

| 参数名称         | 是否必须  | 类型     | 描述                | 默认值   | 取值范围                                     |
| ------------ | ----- | ------ | ----------------- | ----- | ---------------------------------------- |
| symbol       | true  | string | 交易对                |       | btcusdt, ethusdt, ltcusdt, etcusdt, bchusdt, ethbtc, ltcbtc, etcbtc, bchbtc... |
| type         | true  | string | Depth 类型          |       | step0, step1, step2, step3, step4, step5（合并深度0-5）；step0时，不合并深度 |

* 用户选择“合并深度”时，一定报价精度内的市场挂单将予以合并显示。合并深度仅改变显示方式，不改变实际成交价格。

正确订阅例子
```
{
  "sub": "market.btcusdt.depth.step0",
  "id": "id1"
}
```

订阅成功返回数据的例子
```
{
  "id": "id1",
  "status": "ok",
  "subbed": "market.btcusdt.depth.step0",
  "ts": 1489474081631
}
```

之后每当 depth 有更新时，client 会收到数据，例子
```
{
  "ch": "market.btcusdt.depth.step0",
  "ts": 1489474082831,
  "tick": {
    "bids": [
    [9999.3900,0.0098], // [price, amount]
    [9992.5947,0.0560],
    // more Market Depth data here
    ]
    "asks": [
    [10010.9800,0.0099]
    [10011.3900,2.0000]
    //more data here
    ]
  }
}
```

tick 说明
```
  "tick": {
    "bids": [
    [买1价,买1量]
    [买2价,买2量]
    //more data here
    ]
    "asks": [
    [卖1价,卖1量]
    [卖2价,卖2量]
    //more data here
    ]
  }
```

## 请求 Market Depth 数据 market.$symbol.depth.$type 

```
{
  "req": "market.$symbol.depth.$type",
  "id": "id generated by client"
}
```

#### 请求 Market Depth 数据的例子
```
{
  "req": "market.btcusdt.depth.step0",
  "id": "id10"
}
```

返回数据的例子：
```
{
  "rep": "market.btcusdt.depth.step0",
  "status": "ok",
  "id": "id10",
  "tick": {
    "bids": [
    [9999.3900,0.0098], // [price, amount]
    [9992.5947,0.0560],
    // more Market Depth data here
    ]
    "asks": [
    [10010.9800,0.0099]
    [10011.3900,2.0000]
    //more data here
    ]
  }
}
```

## 订阅 Trade Detail 数据 market.$symbol.trade.detail  

```
{
  "sub": "market.$symbol.trade.detail",
  "id": "id generated by client"
}
```

| 参数名称         | 是否必须  | 类型     | 描述                | 默认值   | 取值范围                                     |
| ------------ | ----- | ------ | ----------------- | ----- | ---------------------------------------- |
| symbol       | true  | string | 交易对                |       |btcusdt, ethusdt, ltcusdt, etcusdt, bchusdt, ethbtc, ltcbtc, etcbtc, bchbtc... |

正确订阅例子：

```
{
  "sub": "market.btcusdt.trade.detail",
  "id": "id1"
}
```

订阅成功返回数据的例子：
```
{
  "id": "id1",
  "status": "ok",
  "subbed": "market.btcusdt.trade.detail",
  "ts": 1489474081631
}
```

之后每当 Trade Detail 有更新时，client 会收到数据，例子：

```
{
  "ch": "market.btcusdt.trade.detail",
  "ts": 1489474082831,
  "data": [
    {
      "id":        601595424,
      "price":     10195.64,
      "time":      1494495766,
      "amount":    0.2943,
      "direction": "buy",
      "tradeId":   601595424,
      "ts":        1494495766000
    },
    {
      "id":        601595423,
      "price":     10195.64,
      "time":      1494495711,
      "amount":    0.2430,
      "direction": "buy",
      "tradeId":   601595423,
      "ts":        1494495711000
    },
    // more Trade Detail data here
  ]
  }
}
```

data 说明：
```
  "data": [
    {
      "id":        消息ID,
      "price":     成交价,
      "time":      成交时间,
      "amount":    成交量,
      "direction": 成交方向,
      "tradeId":   成交ID,
      "ts":        时间戳
    }
  ]
```

## 请求 Trade Detail 数据 market.$symbol.trade.detail 

```
{
  "req": "market.$symbol.trade.detail",
  "id": "id generated by client"
}
```

* 仅能获取最近 300 个 Trade Detail 数据

#### 请求 Trade Detail 数据的例子
```
{
  "req": "market.btcusdt.trade.detail",
  "id": "id11"
}
```

返回数据的例子：
```
{
  "rep": "market.btcusdt.trade.detail",
  "status": "ok",
  "id": "id11",
  "data": [
    {
      "id":        601595424,
      "price":     10195.64,
      "time":      1494495766,
      "amount":    0.2943,
      "direction": "buy",
      "tradeId":   601595424,
      "ts":        1494495766000
    },
    {
      "id":        601595423,
      "price":     10195.64,
      "time":      1494495711,
      "amount":    0.2430,
      "direction": "buy",
      "tradeId":   601595423,
      "ts":        1494495711000
    },
    // more Trade Detail data here
  ]
}
```

## 请求 Market Detail 数据 market.$symbol.detail 
```
{
  "req": "market.$symbol.detail",
  "id": "id generated by client"
}
```

* 仅返回当前 Market Detail

#### 请求 Market Detail 数据的例子

```
{
  "req": "market.btcusdt.detail",
  "id": "id12"
}
```

返回数据的例子：
```
{
  "rep": "market.btcusdt.detail",
  "status": "ok",
  "id": "id12",
  "tick": {
    "amount": 12224.2922,
    "open":   9790.52,
    "close":  10195.00,
    "high":   10300.00,
    "ts":     1494496390000,
    "id":     1494496390,
    "count":  15195,
    "low":    9657.00,
    "vol":    121906001.754751
  }
}
```
