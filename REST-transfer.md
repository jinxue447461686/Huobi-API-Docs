##账户内转账 
###transfer
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
        <td>请求的方法 transfer</td>
    </tr>
    <tr>
        <th>access_key</th>
        <td>必填</td>
        <td>访问密匙</td>
    </tr>
    <tr>
        <th>account_from</th>
        <td>必填</td>
        <td>账户类型 1 人民币账户 2 美元账户</td>
    </tr>
    <tr>
        <th>account_to</th>
        <td>必填</td>
        <td>账户类型 1 人民币账户 2 美元账户</td>
    </tr>
    <tr>
        <th>amount</th>
        <td>必填</td>
        <td>转账数量</td>
    </tr>
    <tr>
        <th>coin_type</th>
        <td>必填</td>
        <td>币种 1 比特币（默认）</td>
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
            md5(access_key=xxxxxxxx-xxxxxxxx-xxxxxxxx-xxxxxxxx&amp;account_from=1&amp;account_to=1&amp;amount=xxxxxx&amp;&amp;coin_type=1&amp;created=1386844119&amp;method=transfer&amp;secret_key=xxxxxxxx-xxxxxxxx-xxxxxxxx-xxxxxxxx)
        </td>
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
        <td>转账记录id</td>
    </tr>
    <tr>
        <th>result</th>
        <td>转账结果 成功状态 success</td>
    </tr>
    </tbody>
</table>

