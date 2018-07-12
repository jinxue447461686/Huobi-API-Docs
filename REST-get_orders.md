##获取所有正在进行的委托（当前委托） 
###get_orders
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
        <td>请求的方法 get_orders</td>
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
        <th>sign</th>
        <td>必填</td>
        <td>MD5签名结果</td>
    </tr>
    <tr>
        <th>加密实例</th>
        <td colspan="2">sign =
            md5(access_key=xxxxxxxx-xxxxxxxx-xxxxxxxx-xxxxxxxx&amp;coin_type=1&amp;created=1386844119&amp;method=get_orders&amp;secret_key=xxxxxxxx-xxxxxxxx-xxxxxxxx-xxxxxxxx)
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
        <th>id</th>
        <td>委托订单id</td>
    </tr>
    <tr>
        <th>type</th>
        <td>1买 2卖</td>
    </tr>
    <tr>
        <th>order_price</th>
        <td>委托价格</td>
    </tr>
    <tr>
        <th>order_amount</th>
        <td>委托数量</td>
    </tr>
    <tr>
        <th>processed_amount</th>
        <td>已经完成的数量</td>
    </tr>
    <tr>
        <th>order_time</th>
        <td>委托时间</td>
    </tr>
    </tbody>
</table>

