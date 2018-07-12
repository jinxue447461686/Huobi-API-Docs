##取消提币BTC/LTC 
###cancel_withdraw_coin
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
        <td>请求的方法 cancel_withdraw_coin</td>
    </tr>
    <tr>
        <th>access_key</th>
        <td>必填</td>
        <td>访问密匙</td>
    </tr>
    <tr>
        <th>created</th>
        <td>必填</td>
        <td>提交时间 10位时间戳</td>
    </tr>
    <tr>
        <th>withdraw_coin_id</th>
        <td>必填</td>
        <td>提币申请id</td>
    </tr>
    <tr>
        <th>sign</th>
        <td>必填</td>
        <td>MD5签名结果</td>
    </tr>
    <tr>
        <th>加密实例</th>
        <td colspan="2" style="word-break: break-all;">sign = md5(access_key=xxxxxxxx-xxxxxxxx-xxxxxxxx-xxxxxxxx&amp;created=1386844119&amp;method=cancel_withdraw_coin&amp;secret_key=xxxxxxxx-xxxxxxxx-xxxxxxxx-xxxxxxxx&amp;withdraw_coin_id=123)
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
        <th>code</th>
        <td>正常200，失败时为错误代码</td>
    </tr>
    <tr>
        <th>message</th>
        <td>正常OK，失败时为提示信息</td>
    </tr>
    </tbody>
</table>


