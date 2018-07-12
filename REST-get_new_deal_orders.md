##查询个人最新10条成交订单 
###get_new_deal_orders
####暂不支持美元交易
<table class="table table-bordered">
    <thead>
    <tr>
        <th>字段名</th>
        <th width="12%">填写类型</th>
        <th width="30%">描述</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <th>method</th>
        <td>必填</td>
        <td>请求的方法 get_new_deal_orders</td>
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
        <td colspan="2" style="word-break: break-all;">sign =
            md5(access_key=xxxxxxxx-xxxxxxxx-xxxxxxxx-xxxxxxxx&amp;coin_type=1&amp;created=1386844119&amp;method=get_new_deal_orders&amp;secret_key=xxxxxxxx-xxxxxxxx-xxxxxxxx-xxxxxxxx)
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
        <td>1限价买 2限价卖 3市价买 4市价卖</td>
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
        <td>已经完成的数量（市价买单，代表成交金额）</td>
    </tr>
    <tr>
        <th>last_processed_time</th>
        <td>最后成交时间</td>
    </tr>
    <tr>
        <th>order_time</th>
        <td>委托时间</td>
    </tr>
    <tr>
        <th>status</th>
        <td>状态　0未成交　1部分成交　2已完成　3已取消</td>
    </tr>
    </tbody>
</table>


