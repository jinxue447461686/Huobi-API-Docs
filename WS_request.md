# 请求与订阅说明


### 1. 访问地址

- Pro 站行情请求地址为：wss://api.huobi.pro/ws
- HADAX 站行情请求地址为：wss://api.hadax.com/ws

### 2. 数据压缩
WebSocket API 返回的所有数据都进行了 GZIP 压缩，需要 client 在收到数据之后解压，推荐使用pako。（[【pako】](https://github.com/nodeca/pako) 是一个支持压缩和解压 GZIP 的库）

### 3. WebSocket库
[【ws】](https://github.com/websockets/ws) 是 Node.js 下的 WebSocket 库。

### 4. 心跳
WebSocket API 支持双向心跳，无论是 Server 还是 Client 都可以发起 `ping` message，对方返回 `pong` message。

WebSocket Server 发送心跳：
```
{"ping": 18212558000}
```
 WebSocket Client 应该返回：
```
 {"pong": 18212558000}
```
注：返回的数据里面的 `"pong"` 的值为收到的 `"ping"` 的值
注：WebSocket Client 和 WebSocket Server 建立连接之后，WebSocket Server 每隔 `5s`（这个频率可能会变化） 会向 WebSocket Client 发起一次心跳，WebSocket Client 忽略心跳2次后，WebSocket Server 将会主动断开连接；WebSocket Client发送最近2次心跳message中的其中一个`ping`的值，WebSocket Server都会保持WebSocket连接。
```
┌────────┐                         ┌────────┐ 
│ Client │                         │ Server │
└───┬────┘                         └───┬────┘
    │         {"ping": 18212558000}  │
    │<─────────────────────────────────┤
    │                                  │ wait 5s
    │                                  ├───┐
    │                                  │<──┘
    │         {"ping": 18212558000}  │
    │<─────────────────────────────────┤
    │                                  │
    │ {"pong": 18212558000}          │
    ├┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄>│
    │                                  │
```
注：WebSocket Client 发送最近2次心跳 message 中的其中一个 `"ping"` 的值，WebSocket Server 都会保持 WebSocket 连接
```
┌────────┐                         ┌────────┐ 
│ Client │                         │ Server │
└───┬────┘                         └───┬────┘
    │         {"ping": 1523778470416}  │
    │<─────────────────────────────────┤
    │                                  │ wait 5s
    │                                  ├───┐
    │                                  │<──┘
    │         {"ping": 1523778475416}  │
    │<─────────────────────────────────┤
    │                                  │ wait 5s
    │                                  ├───┐
    │                                  │<──┘
    │                                  │
    │                                  │ close WebSocket connection
    │                                  ├───┐
    │                                  │<──┘
    │                                  │

```
注：WebSocket Client 忽略心跳2次后，WebSocket Server 将会主动断开连接。
WebSocket Client 发送心跳：
```
{"ping": 18212553000}
```
注：发送的 message 里面，"ping" 的值必须为 Long 类型，否则返回错误信息：
```
{
  "ts": 1492420473027,
  "status": "error",
  "err-code": "bad-request",
  "err-msg": "invalid ping"
}
```

WebSocket Server 会返回：
```
{"pong": 18212553000}
```
注：返回的数据里面的 `"pong"` 的值为收到的 `"ping"` 的值

错误信息返回格式
```
{
  "id": "id generate by client",
  "status": "error",
  "err-code": "err-code",
  "err-msg": "err-message",
  "ts": 1487152091345
}
```
注：`ts`为错误信息生成的时间戳，单位：毫秒
### 5. topic格式

订阅数据和请求数据都要使用 `topic`，`topic` 的语法如下：

| topic 类型      | topic 语法                    |sub/req     | 描述                                       |
| ------------- | ---------------------------- | ---------------|------------------------- |
| KLine         | market.$symbol.kline.$period | sub/req |K线 数据，包含单位时间区间的开盘价、收盘价、最高价、最低价、成交量、成交额、成交笔数等数据 $period 可选值：{ 1min, 5min, 15min, 30min, 60min, 4hour,1day, 1mon, 1week, 1year } |
| Market Depth  | market.$symbol.depth.$type   | sub/req |盘口深度，按照不同 step 聚合的买一、买二、买三等和卖一、卖二、卖三等数据 $type 可选值：{ step0, step1, step2, step3, step4, step5, percent10 } （合并深度0-5）；step0时，不合并深度|
| Trade Detail  | market.$symbol.trade.detail  |  sub/req |  成交记录，包含成交价格、成交量、成交方向等信息                                      |
| Market Detail | market.$symbol.detail        |  sub/req |   最近24小时成交量、成交额、开盘价、收盘价、最高价、最低价、成交笔数等                                     |
| Market Tickers | market.tickers  |  sub|   所有对外公开交易对的 日K线、最近24小时成交量等信息                            |

* `$symbol` 为交易对，可选值： { ethbtc, ltcbtc, etcbtc, bchbtc...... }
* 用户选择“合并深度”时，一定报价精度内的市场挂单将予以合并显示。合并深度仅改变显示方式，不改变实际成交价格。

### 6. 请求数据(req/rep)

请求数据，仅返回一次数据

#### 请求数据的格式

```
{
  "req": "topic to req",
  "id": "id generate by client"
}
```
* `"req"` 的值为 **topic** ，请参考 `"5. topic格式"` 的 **topic 格式**

**正确请求数据的例子**

```
{
  "req": "market.btcusdt.kline.1min",
  "id": "id10"
}
```

返回数据的例子：
```
{
  "status": "ok",
  "rep": "market.btcusdt.kline.1min",
  "tick": [
    {
      "amount": 1.6206,
      "count":  3,
      "id":     1494465840,
      "open":   9887.00,
      "close":  9885.00,
      "low":    9885.00,
      "high":   9887.00,
      "vol":    16021.632026
    },
    {
      "amount": 2.2124,
      "count":  6,
      "id":     1494465900,
      "open":   9885.00,
      "close":  9880.00,
      "low":    9880.00,
      "high":   9885.00,
      "vol":    21859.023500
    }
  ]
}
```

**错误请求数据的例子**

```
{
  "req": "market.invalidsymbo.kline.1min",
  "id": "id10"
}
```

返回的错误信息的例子：
```
{
  "status": "error",
  "id": "id10",
  "err-code": "bad-request",
  "err-msg": "invalid topic market.invalidsymbol.trade.detail",
  "ts": 1494483996521
}
```


### 7. 订阅数据(sub)

#### 订阅数据(sub)以及接收订阅数据的大致流程
```
┌────────┐                         ┌────────┐ 
│ Client │                         │ Server │
└───┬────┘                         └───┬────┘
    │ {"sub": "topic"}                 │
    ├─────────────────────────────────>│
    │                                  │
    │              {"subbed": "topic"} │
    │<┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┤
    │                                  │
    │        {"tick": "data of topic"} │
    │<┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┤
    │                                  │
    │        {"tick": "data of topic"} │
    │<┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┤
    │                                  │
```
注：订阅 topic 成功之后，当 topic 对应的数据有更新时，Server 按一定的频率把 topic 对应的新数据推送给 Client
#### 订阅数据的格式

成功建立和 WebSocket API 的连接之后，向 Server 发送如下格式的数据来订阅数据：
```
{
   "id": "id generate by client",
  "sub": "topic to sub",
  "freq-ms": 1000
}
```
注：`id` 参数是可选的
注：`freq-ms` 参数是可选的，可选值为 { `1000`, `2000`, `3000`, `4000`, `5000` }，不传 `freq-ms` 时默认为` 0 `也就是有新的数据就马上推送到 Client，`freq-ms` 决定 Server 推送的频率
**正确订阅的例子**

正确订阅：
```
{
  "sub": "market.btcusdt.kline.1min",
  "id": "id1"
}
```
* `"sub"` 的值为 **topic** ，请参考 `"5. topic格式"` 的 **topic 格式**

订阅成功返回数据的例子：
```
{
  "id": "id1",
  "status": "ok",
  "subbed": "market.btcusdt.kline.1min",
  "ts": 1489474081631
}
```

之后每当 KLine 有更新时，client 会收到数据，例子：
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
tick 说明: 

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

错误订阅（错误的 symbol）：
```
{
  "sub": "market.invalidsymbol.kline.1min",
  "id": "id2"
}
```

订阅失败返回数据的例子：
```
{
  "id": "id2",
  "status": "error",
  "err-code": "bad-request",
  "err-msg": "invalid topic market.invalidsymbol.kline.1min",
  "ts": 1494301904959
}
```

错误订阅（错误的 topic）：
```
{
  "sub": "market.btcusdt.kline.3min",
  "id": "id3"
}
```
订阅失败返回数据的例子：
```
{
  "id": "id3",
  "status": "error",
  "err-code": "bad-request",
  "err-msg": "invalid topic market.btcusdt.kline.3min",
  "ts": 1494310283622
}
```

### 8. 取消订阅(unsub)

#### 取消订阅的格式

WebSocket Client 订阅数据之后，可以取消订阅，取消订阅之后 WebSocket Server 将不会再发送该 topic 的数据，取消订阅的格式如下：

```
{
  "unsub": "topic to unsub",
  "id": "id generate by client"
}
```

**正确取消订阅的例子**

正确取消订阅的例子：
```
{
  "unsub": "market.btcusdt.trade.detail",
  "id": "id4"
}
```

取消订阅成功返回信息的例子：
```
{
  "id": "id4",
  "status": "ok",
  "unsubbed": "market.btcusdt.trade.detail",
  "ts" 1494326028889
}
```

**错误取消订阅的例子**

错误取消订阅的例子（取消订阅一个尚未订阅的 topic）：
```
{
  "unsub": "market.btcusdt.trade.detail",
  "id": "id5"
}
```

返回的错误信息的例子
```
{
  "id": "id5",
  "status": "error",
  "err-code": "bad-request",
  "err-msg": "unsub with not subbed topic market.btcusdt.trade.detail",
  "ts": 1494326217428
}
```

错误取消订阅的例子（取消订阅一个不存在的 topic）：
```
{
  "unsub": "not-exists-topic",
  "id": "id5"
}
```
返回的错误信息的例子：
```
{
  "id": "id5",
  "status": "error",
  "err-code": "bad-request",
  "err-msg": "unsub with not subbed topic not-exists-topic",
  "ts": 1494326318809
}
```
