# 错误码



### 错误信息返回格式
```
{
  "id": "id generate by client",
  "status": "error",
  "err-code": "err-code",
  "err-msg": "err-message",
  "ts": 1487152091345
}
```
注：`"ts"` 为错误信息生成的时间戳，单位：毫秒

| err-msg | 描述 |
| --------- | ------ |
|invalid topic market.invalidsymbol.kline.1min | 错误的 symbol|
|invalid topic market.btccny.kline.3min| 错误的 topic |
| unsub with not subbed topic market.btccny.trade.detail| 取消订阅一个尚未订阅的 topic|
| unsub with not subbed topic not-exists-topic | 取消订阅一个不存在的 topic|
| invalid topic market.invalidsymbol.trade.detail| 错误的 symbol|
