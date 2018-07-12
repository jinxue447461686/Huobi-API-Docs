## 交易 API 请求过程
1. 用户根据文档组织交易要素。

2. 通过POST方式提交交易请求。

3. 请求头信息中必须声明 Content-Type:application/x-www-form-urlencoded

4. 火币网处理请求，并返回相应的JSON格式结果。

5. 交易API目前只支持https请求

6. apiV3 提交地址 https://api.huobi.com/apiv3 

7. 火币网API类似表单提交

8. 生成sign时，参与加密的参数按照a-z排序，签名MD5必须是小写字母。

9. 限制频率（每个接口，只针对交易api，行情api不限制）：withdraw_coin接口访问频率限制为1分钟10次，其余接口限制为10秒100次
 
签名时的字符一律采用UTF-8编码。MD5散列后每个byte采用两个16进制小写字母高位在前低位在后表示。例如： 
```code
md5("比特币你好") = d6b6e11652b0c93c4f14cfb84c380541
md5("ABC123abc") = 85716f0702d2d464803e1366a7678d0b
```