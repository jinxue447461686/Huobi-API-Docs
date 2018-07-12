##根据trade_id查询oder_id 
###get_order_id_by_trade_id
<table class="table table-bordered">
    <thead>
    <tr>
        <th>字段名</th>
        <th>填写类型</th>
        <th>描述</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <th>method</th>
        <td>必填</td>
        <td>请求的方法 get_order_id_by_trade_id</td>
    </tr>
    <tr>
        <th>access_key</th>
        <td>必填</td>
        <td>访问密匙</td>
    </tr>
    <tr>
        <th>coin_type</th>
        <td>必填</td>
        <td>币种 1 比特币 2 莱特币</td>
    </tr>
    <tr>
        <th>created</th>
        <td>必填</td>
        <td>提交时间 10位时间戳</td>
    </tr>
    <tr>
        <th>trade_id</th>
        <td>必填</td>
        <td>调用下单接口时的参数trade_id</td>
    </tr>
    <tr>
        <th>sign</th>
        <td>必填</td>
        <td>MD5签名结果</td>
    </tr>
    <tr>
        <th>加密实例</th>
        <td colspan="2" style="word-break: break-all;">sign = md5(access_key=xxxxxxxx-xxxxxxxx-xxxxxxxx-xxxxxxxx&amp;coin_type=1&amp;created=1386844119&amp;method=get_order_id_by_trade_id&amp;secret_key=xxxxxxxx-xxxxxxxx-xxxxxxxx-xxxxxxxx&amp;trade_id=1)
        </td>
    </tr>
    <tr>
        <th>market</th>
        <td>选填</td>
        <td>此项不参与sign签名过程，交易市场(cny:人民币交易市场，usd:美元交易市场，默认是cny)</td>
    </tr>
    </tbody>
</table>
####返回结果
<table class="table table-bordered">
    <thead>
    <tr>
        <th>字段名</th>
        <th>描述</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <th>order_id</th>
        <td>委托订单id</td>
    </tr>
    </tbody>
</table>


