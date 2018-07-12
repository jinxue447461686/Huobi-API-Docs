##  请求说明

1. 访问地址

Pro 站：
行情： https://api.huobi.pro/market
交易： https://api.huobi.pro/v1

HADAX 站：
行情： https://api.hadax.com/market
交易： https://api.hadax.com/v1

2. POST请求头信息中必须声明 Content-Type:application/json;GET请求头信息中必须声明 Content-Type:application/x-www-form-urlencoded。(汉语用户建议设置 Accept-Language:zh-cn)
3. 所有请求参数请按照 API 说明进行参数封装。
4. 将封装好参数的 API 请求通过 POST 或 GET 的方式提交到服务器。
5. 火币网处理请求，并返回相应的 JSON 格式结果。
6. 请使用 https 请求。
7. 限制频率（每个接口，只针对交易api，行情api不限制）为10秒100次。
8. 查询资产详情方法调用顺序：查询当前用户的所有账户->查询指定账户的余额 
9. 支持所有Pro站上交易中的交易对，上新币保持与网站同步。
