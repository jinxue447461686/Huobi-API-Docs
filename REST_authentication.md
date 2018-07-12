# API 安全认证变更

**重要提示：密钥与账号安全紧密相关，无论何时都请勿向其它人透露

### 变更生效日期：2018年7月9日 14:00:00 （GMT+8 北京时间）

### 变更过渡期：2018年7月23日 23:59:59 （GMT+8 北京时间）

## 当前状态
目前关于apikey申请和修改，请在“账户 - API管理”页面进行相关操作。其中AccessKey为API 访问密钥，SecretKey为用户对请求进行签名的密钥（仅申请时可见）。在对有验签要求的API发出请求时，需包括Signature参数。Pro站和HADAX站apikey通用。

## 变更概要
•	用户需自己生成Private Key和Public Key，Private Key由用户自己保存，用户需在API管理页面中提供Public Key (参见变更后细节1，2）。

•	用户按原规则生成签名(Signature)，然后使用ECDSA算法和Private Key对签名加签生成私钥签名(PrivateSignature)（参见变更后细节3.3），请求结构中需同时包括Signature 和PrivateSignature，其他流程不变。（参见变更后细节4，以及APPENDIX DEMO）

## 对现有用户的影响
•	在变更过渡期间，原有验签方法仍然有效，兼容请求结构中缺省PrivateSignature参数的情况。

•	自变更生效日起，用户即可对现有API Key关联Public Key，或者新创建API Key。

•	自变更生效日起，用户即可使用新的签名方法（Signature 和 PrivateSignature). 

## 变更后细节

**重要提示：密钥与账号安全紧密相关，无论何时都请勿向其它人透露

### 1.	生成Private Key和Public Key
请参考[使用OpenSSL工具生成密钥](https://github.com/huobiapi/API-FAQ/wiki/Create_User_Keys)
### 2.	关联Public Key或重新创建API Key
2.1.	用户可以在API管理通过编辑现有的API Key，关联Public Key。在过渡期到期时，如果某一API Key还没有关联Public Key，该API Key将不可用。
2.2.	用户也可重新创建API Key。在重新创建API Key时，需提供Public Key。
如下图：

<img width="881" alt="screen shot 2018-07-05 at 1 06 24 pm" src="https://user-images.githubusercontent.com/9877081/42428395-05e1b5b2-8366-11e8-84cb-2f955e11ce9b.png">

创建成功后，系统返回AccessKey和SecretKey （与现有流程相同）

<img width="559" alt="screen shot 2018-07-05 at 1 51 07 pm" src="https://user-images.githubusercontent.com/9877081/42428426-2998a1aa-8366-11e8-8914-5cad8e292516.png">

### 3.	生成Signature 和 PrivateSignature

API 请求在通过 Internet 发送的过程中极有可能被篡改。为了确保请求未被更改，我们会要求用户在每个请求中带上签名（行情 API 除外），来校验参数或参数值在传输途中是否发生了更改。
   
3.1. 规范要计算签名的请求
因为使用 HMAC 进行签名计算时，使用不同内容计算得到的结果会完全不同。所以在进行签名计算前，请先对请求进行规范化处理。
下面以查询某订单详情请求为例进行说明


```
https://api.huobi.pro/v1/order/orders?
AccessKeyId=e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx
&SignatureMethod=HmacSHA256
&SignatureVersion=2
&Timestamp=2017-05-11T15:19:30 //您发出请求的时间 YYYY-MM-DDTHH:MM:SS(UTC 时区)。
&order-id=1234567890
```
3.1.1. 首先请求方法（GET 或 POST），后面添加换行符\n。
```
GET\n
```
3.1.2. 然后添加小写的访问地址，后面添加换行符\n。
```
api.huobi.pro\n
```
3.1.3. 在访问方法的路径，后面添加换行符\n。
```
/v1/order/orders\n
```
3.1.4. 接下来按以下步骤构造一个URL查询字符串（URL query string）。按照**ASCII码的顺序对请求参数名进行排序**(**使用 UTF-8 编码**，**且进行了 URI 编码**，**十六进制字符必须大写**，如‘:’会被编码为'%3A'，空格被编码为'%20')。
例如，下面是请求参数的原始顺序。
```
AccessKeyId=e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx
order-id=1234567890
SignatureMethod=HmacSHA256
SignatureVersion=2
Timestamp=2017-05-11T15%3A19%3A30
```
进行过编码后，这些参数会被排序为：
```
AccessKeyId=e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx
SignatureMethod=HmacSHA256
SignatureVersion=2
Timestamp=2017-05-11T15%3A19%3A30
order-id=1234567890
```
然后按照以上顺序，将各参数使用字符’&’连接。
```
AccessKeyId=e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx&SignatureMethod=HmacSHA256&SignatureVersion=2&Timestamp=2017-05-11T15%3A19%3A30&order-id=1234567890
```
3.1.5. 最后组成最终的要进行签名计算的字符串如下：
```
GET\n
api.huobi.pro\n
/v1/order/orders\n
AccessKeyId=e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx&SignatureMethod=HmacSHA256&SignatureVersion=2&Timestamp=2017-05-11T15%3A19%3A30&order-id=1234567890
```
3.2. 计算签名

将以下两个参数传入加密哈希函数进行计算

- 需要进行签名计算的字符串 （section3.1得到的结果）
```
GET\n
api.huobi.pro\n
/v1/order/orders\n
AccessKeyId=e2xxxxxx-99xxxxxx-84xxxxxx-7xxxx&SignatureMethod=HmacSHA256&SignatureVersion=2&Timestamp=2017-05-11T15%3A19%3A30&order-id=1234567890
```
- 进行签名所需的SecretKey （创建API Key 成功时返回的SecretKey）
```
b0xxxxxx-c6xxxxxx-94xxxxxx-dxxxx
```
- 将得到的计算结果进行 Base64编码，得到Signature
```
4F65x5A2bLyMWVQj3Aqp+B4w+ivaA7n5Oi2SuYtCJ9o=
```
3.3.	计算私钥签名（新步骤）

将3.2计算得到的Signature 和Private Key传入加密哈希函数进行计算，得到的计算结果进行Base64编码得到最终的PrivateSignature 

### 4. API请求时包含Signature 和 PrivateSignature参数

 将Section 3 得到Signature 和PrivateSignature先进行URI编码成为URL查询字符串（URL query string），然后添加到 API 请求中.

基于安全考虑，除行情API 外的 API 请求都必须进行签名运算。一个合法的请求由以下几部分组成：

 - 服务请求地址
   即访问服务器地址：api.huobi.pro或者api.hadax.com后面跟上服务名称，比如api.huobi.pro/v1/order/orders。

 - AccessKey（AccessKeyId）
   您申请的 API KEY 中的AccessKey。

 - 签名方法（SignatureMethod）
   用户计算签名的基于哈希的协议，此处使用 HmacSHA256。

 - 签名版本（SignatureVersion）
   签名协议的版本，此处使用2。

 - 时间戳（Timestamp）
   您发出请求的时间 YYYY-MM-DDTHH:MM:SS(UTC 时区) 。在查询请求中包含此值有助于防止第三方截取您的请求。如：2017-05-11T16:22:06。再次强调是 **(UTC 时区)** 。

 - 必选和可选参数
   每个请求方法都有一组必需请求参数和可选请求参数。请参照API Reference中每个方法的说明中查看这些参数及其含义。

   请一定注意：
   对于**GET**请求，每个方法自带的参数都需要包含在签名运算中；

   对于**POST**请求，每个方法自带的参数不需要包含在签名认证中，即**POST**请求中需要进行签名运算的只有AccessKeyId、SignatureMethod、SignatureVersion、Timestamp四个参数，其它参数放在body中。

 - 签名 (Signature, 3.2.得到的结果)
   签名计算得出的值，用于确保签名有效和未被篡改。

- 私钥签名 (新要求。PrivateSignature, 3.3. 得到的结果)
使用ECDSA算法和私钥对签名(Signature)加签产生的PrivateSignature。

请求示例：
```
http://api.huobi.pro/v1/account/accounts?AccessKeyId=f70d805f-2467cb8a-3d40d7bd-a50f7&SignatureMethod=HmacSHA256&SignatureVersion=2&Timestamp=2018-07-05T08:26:22&Signature=85WuwICm8gypsc5a/qTvWBs2EaKzNevscan4IH9P5v4=&PrivateSignature=ybFd+VTwfX6SPP92hbwnjGpycW6und6lbHdPeW1PJV5necpj1sn7+iTxxbTeF+SZG1fdc3uMQ/JRw8UumG0e/g==
```

#### 响应码说明

| 错误代码 | 英文说明 | 中文说明 | 类型 |
| ------- | ----- | ---- | ---- |
| 500 | System error | 系统错误 | M |
|502	|Parameter error	|参数错误	|M|
|12001	|Invalid submission time or incorrect time format	|无效的提交时间，或时间格式错误	|M|
|12002	|Incorrect signature version	|错误的签名版本	|M|
|12003	|Incorrect signature method	|错误的签名方法	|M|
|12004	|API key has expired	|API Key已经过期	|M|
|12005	|Incorrect IP address	|ip地址错误	|M|
|12006	|Submission time is required	|提交时间不能为空	|M|
|12007	|Incorrect Access key	|Access key错误	|M|
|12008	|Verification failure	|校验失败	|M|
|12009	|Abnormal user status	|用户状态不正常	|M|
|12010	|Incorrect Private Key signature	|Private Key签名错误	|M|
|12011	|Incorrect Public key	|Public key错误	|M|

#### 响应示例

```json
{
    "status":"error",
    "err-code":"api-signature-not-valid",
    "err-msg":"Signature not valid: Invalid submission time or incorrect time format [无效的提交时间，或时间格式错误]",
    "data":null
}
```

### APPENDIX DEMO

1. [REST-Java-demo](https://github.com/huobiapi/REST-API-demos/tree/master/REST-Java-demo)
2. [Rest-C#-demo](https://github.com/huobiapi/REST-API-demos/tree/master/Rest-C%23-demo)
3. [REST-Python3-demo](https://github.com/huobiapi/REST-API-demos/tree/master/REST-Python3-demo)
