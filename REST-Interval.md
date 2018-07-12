##分时行情数据接口（K线）
`目前支持人民币现货、美元现货`
###数据文件：
[BTC-CNY] `http://api.huobi.com/staticmarket/btc_kline_[period]_json.js`

[LTC-CNY] `http://api.huobi.com/staticmarket/ltc_kline_[period]_json.js`

[BTC-USD] `http://api.huobi.com/usdmarket/btc_kline_[period]_json.js`

<table class="table table-bordered">
    <thead>
    <tr>
        <th width='25%'>period 参数</th>
        <th>说明</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <th>001</th>
        <td>1分钟线</td>
    </tr>
    <tr>
        <th>005</th>
        <td>5分钟</td>
    </tr>
    <tr>
        <th>015</th>
        <td>15分钟</td>
    </tr>
    <tr>
        <th>030</th>
        <td>30分钟</td>
    </tr>
    <tr>
        <th>060</th>
        <td>60分钟</td>
    </tr>
    <tr>
        <th>100</th>
        <td>日线</td>
    </tr>
    <tr>
        <th>200</th>
        <td>周线</td>
    </tr>
    <tr>
        <th>300</th>
        <td>月线</td>
    </tr>
    <tr>
        <th>400</th>
        <td>年线</td>
    </tr>
    <tr>
    	<th>例如</th>
        <td>
            [BTC-CNY] http://api.huobi.com/staticmarket/btc_kline_005_json.js<br>
            [LTC-LTC] http://api.huobi.com/staticmarket/ltc_kline_005_json.js<br>
            [BTC-USD] http://api.huobi.com/usdmarket/btc_kline_005_json.js
        </td>
    </tr>
    </tbody>
</table>


<table class="table table-bordered">
    <thead>
    <tr>
        <th width='25%'>length参数</th>
        <th>说明</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <th>1~2000</th>
        <td>返回1~2000条数据，如果不传该参数默认为300条</td>
    </tr>
    <tr>
    	<th>例如</th>
        <td>
            [BTC-CNY] http://api.huobi.com/staticmarket/btc_kline_005_json.js?length=500<br>

        </td>
    </tr>
    </tbody>
</table>

###数据格式:（json）
```javascript
[["20140417095000000",3297,3305,3290,3303,386.3926],...]
```

日期时间，开盘价，最高价，最低价，收盘价，成交量
###用例：
![行情图例](https://static.huobi.com/img/help/market_help_img1.png)
