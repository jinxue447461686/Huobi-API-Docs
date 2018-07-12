## REST API 简介

火币为用户提供了一套全新的API，可以帮用户快速接入火币PRO站及HADAX站的交易系统，实现程序化交易。

| 访问地址 | 适用站点 | 适用功能 | 适用交易对 |
|----|----|----|----|
| https://api.huobi.pro/market|火币PRO  |    行情    | 所有Pro站交易中的交易对  |
| https://api.huobi.pro/v1|火币PRO  |   交易     | 同上  |
| https://api.hadax.com/market| HADAX hadax.com|    行情    | 所有HADAX站交易中的交易对  |
| https://api.hadax.com/v1| HADAX hadax.com|   交易     | 同上  |

通过API可以实现以下功能：

- 市场行情信息查询（K线、深度、实时成交、24小时行情）
- 账户资产信息查询
- 下单、撤单操作 
- 订单信息查询
  所有请求基于 HTTPS 协议。在使用中如果遇到问题，请加技术讨论 QQ 群:  火币网API交流群(6) 782369511（加群时请注明uid和编程语言），我们将尽力帮您答疑解惑。
