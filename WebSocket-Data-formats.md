##3.数据格式
###3.1请求地址
行情服务器地址：hq.huobi.com:80

###3.2行情接口介绍
####1)	获取交易代码列表


	reqSymbolList该接口主要获取交易代码列表以及基本信息。每一条信息只包含一条或者多条交易代码的基本信息。<br>
	终端向实时行情服务器请求消息格式如下：

<table class="table table-bordered">
	<thead>
		<tr>
			<th style="width: 200px;">接口名称</th>
			<th>字段名称</th>
			<th style="width: 60px;">是否可选</th>
			<th>字段值</th>
			<th>字段说明</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<th rowspan="4">获取交易代码列表</th>
			<th>version</th>
			<td>必选</td>
			<td>1</td>
			<td>终端版本</td>
		</tr>
		<tr>
			<th>msgType</th>
			<td>必选</td>
			<td>reqSymbolList</td>
			<td>消息类型</td>
		</tr>
		<tr>
			<th>requestIndex</th>
			<td>可选</td>
			<td>100</td>
			<td>请求序列号，方便判断多个请求的先后顺序，终端发送的数据，服务端会返回相同的数据</td>
		</tr>
		<tr>
			<th>symbolIdList</th>
			<td>可选</td>
			<td>[btccny,ltccny,btcusd]</td>
			<td>交易代码列表，零到多个交易编码。如果为空，则返回所有的交易编码</td>
		</tr>
	</tbody>
</table>

实时行情服务器向终端回应消息格式如下：
<table class="table table-bordered">
	<thead>
		<tr>
			<th style="width: 200px;">接口名称</th>
			<th>字段名称</th>
			<th style="width: 60px;">是否可选</th>
			<th>字段值</th>
			<th>字段说明</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<th rowspan="6">获取交易代码列表</th>
			<th>version</th>
			<td>必选</td>
			<td>1</td>
			<td>终端版本</td>
		</tr>
		<tr>
			<th>msgType</th>
			<td>必选</td>
			<td>reqSymbolList</td>
			<td>消息类型</td>
		</tr>
		<tr>
			<th>requestIndex</th>
			<td>可选</td>
			<td>100</td>
			<td>请求序列号，方便判断多个请求的先后顺序，终端发送的数据，服务端会返回相同的数据</td>
		</tr>
		<tr>
			<th>retCode</th>
			<td>必选</td>
			<td>200</td>
			<td>返回错误码，200为成功，其他的参照http返回码</td>
		</tr>
		<tr>
			<th>retMsg</th>
			<td>必选</td>
			<td>成功</td>
			<td>返回消息</td>
		</tr>
		<tr>
			<th>payload</th>
			<td>必选</td>
			<td></td>
			<td>有效数据</td>
		</tr>
	</tbody>
</table>

####2)	获取交易代码详细信息


	reqSymbolDetail该接口主要在已知交易代码下，获取交易代码的详细信息。每一条信息只包含一条或者多条交易代码的详细信息。<br>
	终端向实时行情服务器请求消息格式如下：

<table class="table table-bordered">
	<thead>
		<tr>
			<th style="width: 200px;">接口名称</th>
			<th>字段名称</th>
			<th style="width: 60px;">是否可选</th>
			<th>字段值</th>
			<th>字段说明</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<th rowspan="4">获取交易代码详细信息</th>
			<th>version</th>
			<td>必选</td>
			<td>1</td>
			<td>终端版本</td>
		</tr>
		<tr>
			<th>msgType</th>
			<td>必选</td>
			<td>reqSymbolDetail</td>
			<td>消息类型</td>
		</tr>
		<tr>
			<th>requestIndex</th>
			<td>可选</td>
			<td>100</td>
			<td>请求序列号，方便判断多个请求的先后顺序，终端发送的数据，服务端会返回相同的数据</td>
		</tr>
		<tr>
			<th>symbolIdList</th>
			<td>必选</td>
			<td>[btccny,ltccny,btcusd]</td>
			<td>交易代码列表，1个到多个交易编码</td>
		</tr>
	</tbody>
</table>
实时行情服务器向终端回应消息格式如下：
<table class="table table-bordered">
	<thead>
		<tr>
			<th style="width: 200px;">接口名称</th>
			<th>字段名称</th>
			<th style="width: 60px;">是否可选</th>
			<th>字段值</th>
			<th>字段说明</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<th rowspan="6">获取交易代码详细信息</th>
			<th>version</th>
			<td>必选</td>
			<td>1</td>
			<td>终端版本</td>
		</tr>
		<tr>
			<th>msgType</th>
			<td>必选</td>
			<td>reqSymbolDetail</td>
			<td>消息类型</td>
		</tr>
		<tr>
			<th>requestIndex</th>
			<td>可选</td>
			<td>100</td>
			<td>请求序列号，方便判断多个请求的先后顺序，终端发送的数据，服务端会返回相同的数据</td>
		</tr>
		<tr>
			<th>retCode</th>
			<td>必选</td>
			<td>200</td>
			<td>返回错误码，200为成功，其他的参照http返回码</td>
		</tr>
		<tr>
			<th>retMsg</th>
			<td>必选</td>
			<td>成功</td>
			<td>返回消息</td>
		</tr>
		<tr>
			<th>payload</th>
			<td>必选</td>
			<td></td>
			<td>有效数据</td>
		</tr>
	</tbody>
</table>

####3)	推送消息注册


	reqMsgSubscribe该接口提供推送消息注册。消息以交易代码加上消息类型为基本单元。消息可以注册多次，以最后一次注册为准。<br>
	终端向实时行情服务器请求消息格式如下：

<table class="table table-bordered">
	<thead>
		<tr>
			<th style="width: 200px;">接口名称</th>
			<th>字段名称</th>
			<th style="width: 60px;">是否可选</th>
			<th>字段值</th>
			<th>字段说明</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<th rowspan="4">推送消息注册</th>
			<th>version</th>
			<td>必选</td>
			<td>1</td>
			<td>终端版本</td>
		</tr>
		<tr>
			<th>msgType</th>
			<td>必选</td>
			<td>reqMsgSubscribe</td>
			<td>消息类型</td>
		</tr>
		<tr>
			<th>requestIndex</th>
			<td>可选</td>
			<td>100</td>
			<td>请求序列号，方便判断多个请求的先后顺序，终端发送的数据，服务端会返回相同的数据</td>
		</tr>
		<tr>
			<th>symbolIdList</th>
			<td>必选</td>
			<td>{消息名称:[{"symbolId":数组,"pushType":数组,"period":k线周期数组,"percent":深度百分比数组}]}</td>
			<td>需要推送的交易代码列表。一个或者多个交易编码。每一个推送请求包括“交易代码，消息类型，推送策略”</td>
		</tr>
	</tbody>
</table>
实时行情服务器向终端回应消息格式如下：
<table class="table table-bordered">
	<thead>
		<tr>
			<th style="width: 200px;">接口名称</th>
			<th>字段名称</th>
			<th style="width: 60px;">是否可选</th>
			<th>字段值</th>
			<th>字段说明</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<th rowspan="5">推送消息注册</th>
			<th>version</th>
			<td>必选</td>
			<td>1</td>
			<td>终端版本</td>
		</tr>
		<tr>
			<th>msgType</th>
			<td>必选</td>
			<td>reqMsgSubscribe</td>
			<td>消息类型</td>
		</tr>
		<tr>
			<th>requestIndex</th>
			<td>可选</td>
			<td>100</td>
			<td>请求序列号，方便判断多个请求的先后顺序，终端发送的数据，服务端会返回相同的数据</td>
		</tr>
		<tr>
			<th>retCode</th>
			<td>必选</td>
			<td>200</td>
			<td>返回错误码，200为成功，其他的参照http返回码</td>
		</tr>
		<tr>
			<th>retMsg</th>
			<td>必选</td>
			<td>成功</td>
			<td>返回消息</td>
		</tr>
	</tbody>
</table>

####4)	推送消息注销


	reqMsgUnsubscribe该接口提供推送消息注销。消息以交易代码加上消息类型为基本单元。消息可以注册多次，只需要注销一次，对于短效消息，可以不显示取消，后注册的短效消息会覆盖之前的。<br>
	终端向实时行情服务器请求消息格式如下：

<table class="table table-bordered">
	<thead>
		<tr>
			<th style="width: 200px;">接口名称</th>
			<th>字段名称</th>
			<th style="width: 60px;">是否可选</th>
			<th>字段值</th>
			<th>字段说明</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<th rowspan="4">推送消息注销</th>
			<th>version</th>
			<td>必选</td>
			<td>1</td>
			<td>终端版本</td>
		</tr>
		<tr>
			<th>msgType</th>
			<td>必选</td>
			<td>reqMsgUnsubscribe</td>
			<td>消息类型</td>
		</tr>
		<tr>
			<th>requestIndex</th>
			<td>可选</td>
			<td>100</td>
			<td>请求序列号，方便判断多个请求的先后顺序，终端发送的数据，服务端会返回相同的数据</td>
		</tr>
		<tr>
			<th>symbolIdList</th>
			<td>必选</td>
			<td>{消息名称:[{"symbolId":数组,"period":k线周期数组,"percent":深度百分比数组}]}</td>
			<td>需要注销推送的交易代码列表。一个或者多个交易编码。每一个推送请求包括“交易代码，消息类型，推送策略”</td>
		</tr>
	</tbody>
</table>
实时行情服务器向终端回应消息格式如下：
<table class="table table-bordered">
	<thead>
		<tr>
			<th style="width: 200px;">接口名称</th>
			<th>字段名称</th>
			<th style="width: 60px;">是否可选</th>
			<th>字段值</th>
			<th>字段说明</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<th rowspan="5">推送消息注销</th>
			<th>version</th>
			<td>必选</td>
			<td>1</td>
			<td>终端版本</td>
		</tr>
		<tr>
			<th>msgType</th>
			<td>必选</td>
			<td>reqMsgUnsubscribe</td>
			<td>消息类型</td>
		</tr>
		<tr>
			<th>requestIndex</th>
			<td>可选</td>
			<td>100</td>
			<td>请求序列号，方便判断多个请求的先后顺序，终端发送的数据，服务端会返回相同的数据</td>
		</tr>
		<tr>
			<th>retCode</th>
			<td>必选</td>
			<td>200</td>
			<td>返回错误码，200为成功，其他的参照http返回码</td>
		</tr>
		<tr>
			<th>retMsg</th>
			<td>必选</td>
			<td>成功</td>
			<td>返回消息</td>
		</tr>
	</tbody>
</table>

####5)	获取历史分时数据


	reqTimeLine获取历史分时的数据，默认最近300条的时间区间。<br>
	终端向实时行情服务器请求消息格式如下：

<table class="table table-bordered">
	<thead>
		<tr>
			<th style="width: 200px;">接口名称</th>
			<th>字段名称</th>
			<th style="width: 60px;">是否可选</th>
			<th>字段值</th>
			<th>字段说明</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<th rowspan="6">获取历史分时数据</th>
			<th>version</th>
			<td>必选</td>
			<td>1</td>
			<td>终端版本</td>
		</tr>
		<tr>
			<th>msgType</th>
			<td>必选</td>
			<td>reqTimeLine</td>
			<td>消息类型</td>
		</tr>
		<tr>
			<th>requestIndex</th>
			<td>可选</td>
			<td>100</td>
			<td>请求序列号，方便判断多个请求的先后顺序，终端发送的数据，服务端会返回相同的数据</td>
		</tr>
		<tr>
			<th>symbolId</th>
			<td>必选</td>
			<td>btccny</td>
			<td>交易代码列表，零到多个交易编码。</td>
		</tr>
		<tr>
			<th>from</th>
			<td>可选</td>
			<td></td>
			<td>开始时间，默认最近300条的时间区间。</td>
		</tr>
		<tr>
			<th>to</th>
			<td>可选</td>
			<td></td>
			<td>结束时间，默认到最新。</td>
		</tr>
	</tbody>
</table>
实时行情服务器向终端回应消息格式如下：
<table class="table table-bordered">
	<thead>
		<tr>
			<th style="width: 200px;">接口名称</th>
			<th>字段名称</th>
			<th style="width: 60px;">是否可选</th>
			<th>字段值</th>
			<th>字段说明</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<th rowspan="6">获取历史分时数据</th>
			<th>version</th>
			<td>必选</td>
			<td>1</td>
			<td>终端版本</td>
		</tr>
		<tr>
			<th>msgType</th>
			<td>必选</td>
			<td>reqTimeLine</td>
			<td>消息类型</td>
		</tr>
		<tr>
			<th>requestIndex</th>
			<td>可选</td>
			<td>100</td>
			<td>请求序列号，方便判断多个请求的先后顺序，终端发送的数据，服务端会返回相同的数据</td>
		</tr>
		<tr>
			<th>retCode</th>
			<td>必选</td>
			<td>200</td>
			<td>返回错误码，200为成功，其他的参照http返回码</td>
		</tr>
		<tr>
			<th>retMsg</th>
			<td>必选</td>
			<td>成功</td>
			<td>返回消息</td>
		</tr>
		<tr>
			<th>payload</th>
			<td>必选</td>
			<td></td>
			<td>有效数据</td>
		</tr>
	</tbody>
</table>

####6)	获取历史k线信息


	reqKLine获取历史k线信息，默认最近300条的时间区间。<br>
	终端向实时行情服务器请求消息格式如下：

<table class="table table-bordered">
	<thead>
		<tr>
			<th style="width: 200px;">接口名称</th>
			<th>字段名称</th>
			<th style="width: 60px;">是否可选</th>
			<th>字段值</th>
			<th>字段说明</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<th rowspan="7">获取历史k线信息</th>
			<th>version</th>
			<td>必选</td>
			<td>1</td>
			<td>终端版本</td>
		</tr>
		<tr>
			<th>msgType</th>
			<td>必选</td>
			<td>reqKLine</td>
			<td>消息类型</td>
		</tr>
		<tr>
			<th>requestIndex</th>
			<td>可选</td>
			<td>100</td>
			<td>请求序列号，方便判断多个请求的先后顺序，终端发送的数据，服务端会返回相同的数据</td>
		</tr>
		<tr>
			<th>symbolId</th>
			<td>必选</td>
			<td>btccny</td>
			<td>交易代码列表，1个到多个交易编码。</td>
		</tr>
		<tr>
			<th>period</th>
			<td>必选</td>
			<td></td>
			<td>K线类型</td>
		</tr>
		<tr>
			<th>from</th>
			<td>可选</td>
			<td></td>
			<td>开始时间，默认最近300条的时间区间。</td>
		</tr>
		<tr>
			<th>to</th>
			<td>可选</td>
			<td></td>
			<td>结束时间，默认到最新。当取值为-1时返回最近300条</td>
		</tr>
	</tbody>
</table>
实时行情服务器向终端回应消息格式如下：
<table class="table table-bordered">
	<thead>
		<tr>
			<th style="width: 200px;">接口名称</th>
			<th>字段名称</th>
			<th style="width: 60px;">是否可选</th>
			<th>字段值</th>
			<th>字段说明</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<th rowspan="7">获取历史分时数据</th>
			<th>version</th>
			<td>必选</td>
			<td>1</td>
			<td>终端版本</td>
		</tr>
		<tr>
			<th>msgType</th>
			<td>必选</td>
			<td>reqTimeLine</td>
			<td>消息类型</td>
		</tr>
		<tr>
			<th>requestIndex</th>
			<td>可选</td>
			<td>100</td>
			<td>请求序列号，方便判断多个请求的先后顺序，终端发送的数据，服务端会返回相同的数据</td>
		</tr>
		<tr>
			<th>retCode</th>
			<td>必选</td>
			<td>200</td>
			<td>返回错误码，200为成功，其他的参照http返回码</td>
		</tr>
		<tr>
			<th>retMsg</th>
			<td>必选</td>
			<td>成功</td>
			<td>返回消息</td>
		</tr>
		<tr>
			<th>period</th>
			<td>必选</td>
			<td></td>
			<td>k线类型</td>
		</tr>
		<tr>
			<th>payload</th>
			<td>必选</td>
			<td></td>
			<td>有效数据</td>
		</tr>
	</tbody>
</table>

####7)	获取Top行情深度


	reqMarketDepthTop该消息用于获取完整的Top行情深度。<br>
	终端向实时行情服务器请求消息格式如下：

<table class="table table-bordered">
	<thead>
		<tr>
			<th style="width: 200px;">接口名称</th>
			<th>字段名称</th>
			<th style="width: 60px;">是否可选</th>
			<th>字段值</th>
			<th>字段说明</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<th rowspan="4">获取Top行情深度</th>
			<th>version</th>
			<td>必选</td>
			<td>1</td>
			<td>终端版本</td>
		</tr>
		<tr>
			<th>msgType</th>
			<td>必选</td>
			<td>reqMarketDepthTop</td>
			<td>消息类型</td>
		</tr>
		<tr>
			<th>requestIndex</th>
			<td>可选</td>
			<td>100</td>
			<td>请求序列号，方便判断多个请求的先后顺序，终端发送的数据，服务端会返回相同的数据</td>
		</tr>
		<tr>
			<th>symbolId</th>
			<td>必选</td>
			<td>btccny</td>
			<td>交易代码列表，1个到多个交易编码。</td>
		</tr>
	</tbody>
</table>
实时行情服务器向终端回应消息格式如下：
<table class="table table-bordered">
	<thead>
		<tr>
			<th style="width: 200px;">接口名称</th>
			<th>字段名称</th>
			<th style="width: 60px;">是否可选</th>
			<th>字段值</th>
			<th>字段说明</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<th rowspan="7">获取Top行情深度</th>
			<th>version</th>
			<td>必选</td>
			<td>1</td>
			<td>终端版本</td>
		</tr>
		<tr>
			<th>msgType</th>
			<td>必选</td>
			<td>reqMarketDepthTop</td>
			<td>消息类型</td>
		</tr>
		<tr>
			<th>requestIndex</th>
			<td>可选</td>
			<td>100</td>
			<td>请求序列号，方便判断多个请求的先后顺序，终端发送的数据，服务端会返回相同的数据</td>
		</tr>
		<tr>
			<th>retCode</th>
			<td>必选</td>
			<td>200</td>
			<td>返回错误码，200为成功，其他的参照http返回码</td>
		</tr>
		<tr>
			<th>retMsg</th>
			<td>必选</td>
			<td>成功</td>
			<td>返回消息</td>
		</tr>
		<tr>
			<th>version</th>
			<td>可选</td>
			<td></td>
			<td>快照版本</td>
		</tr>
		<tr>
			<th>payload</th>
			<td>必选</td>
			<td></td>
			<td>有效数据</td>
		</tr>
	</tbody>
</table>

####8)	获取行情深度


	reqMarketDepth该消息用于获取完整的行情深度。<br>
	终端向实时行情服务器请求消息格式如下：

<table class="table table-bordered">
	<thead>
		<tr>
			<th style="width: 200px;">接口名称</th>
			<th>字段名称</th>
			<th style="width: 60px;">是否可选</th>
			<th>字段值</th>
			<th>字段说明</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<th rowspan="5">获取Top行情深度</th>
			<th>version</th>
			<td>必选</td>
			<td>1</td>
			<td>终端版本</td>
		</tr>
		<tr>
			<th>msgType</th>
			<td>必选</td>
			<td>reqMarketDepthTop</td>
			<td>消息类型</td>
		</tr>
		<tr>
			<th>requestIndex</th>
			<td>可选</td>
			<td>100</td>
			<td>请求序列号，方便判断多个请求的先后顺序，终端发送的数据，服务端会返回相同的数据</td>
		</tr>
		<tr>
			<th>symbolId</th>
			<td>必选</td>
			<td>btccny</td>
			<td>交易代码列表，1个到多个交易编码。</td>
		</tr>
		<tr>
			<th>percent</th>
			<td>必选</td>
			<td></td>
			<td>行情深度的百分比，缺省10%</td>
		</tr>
	</tbody>
</table>
实时行情服务器向终端回应消息格式如下：
<table class="table table-bordered">
	<thead>
		<tr>
			<th style="width: 200px;">接口名称</th>
			<th>字段名称</th>
			<th style="width: 60px;">是否可选</th>
			<th>字段值</th>
			<th>字段说明</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<th rowspan="6">获取Top行情深度</th>
			<th>version</th>
			<td>必选</td>
			<td>1</td>
			<td>终端版本</td>
		</tr>
		<tr>
			<th>msgType</th>
			<td>必选</td>
			<td>reqMarketDepthTop</td>
			<td>消息类型</td>
		</tr>
		<tr>
			<th>requestIndex</th>
			<td>可选</td>
			<td>100</td>
			<td>请求序列号，方便判断多个请求的先后顺序，终端发送的数据，服务端会返回相同的数据</td>
		</tr>
		<tr>
			<th>retCode</th>
			<td>必选</td>
			<td>200</td>
			<td>返回错误码，200为成功，其他的参照http返回码</td>
		</tr>
		<tr>
			<th>version</th>
			<td>可选</td>
			<td></td>
			<td>快照版本</td>
		</tr>
		<tr>
			<th>payload</th>
			<td>必选</td>
			<td></td>
			<td>有效数据</td>
		</tr>
	</tbody>
</table>

####9)	获取Top交易明细


	reqTradeDetailTop该消息用于获取完整的行情深度。<br>
	终端向实时行情服务器请求消息格式如下：

<table class="table table-bordered">
	<thead>
		<tr>
			<th style="width: 200px;">接口名称</th>
			<th>字段名称</th>
			<th style="width: 60px;">是否可选</th>
			<th>字段值</th>
			<th>字段说明</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<th rowspan="5">获取Top交易明细</th>
			<th>version</th>
			<td>必选</td>
			<td>1</td>
			<td>终端版本</td>
		</tr>
		<tr>
			<th>msgType</th>
			<td>必选</td>
			<td>reqTradeDetailTop</td>
			<td>消息类型</td>
		</tr>
		<tr>
			<th>requestIndex</th>
			<td>可选</td>
			<td>100</td>
			<td>请求序列号，方便判断多个请求的先后顺序，终端发送的数据，服务端会返回相同的数据</td>
		</tr>
		<tr>
			<th>symbolId</th>
			<td>必选</td>
			<td>btccny</td>
			<td>交易代码列表，1个到多个交易编码。</td>
		</tr>
		<tr>
			<th>Count</th>
			<td>可选</td>
			<td></td>
			<td>获取明细条数，缺省50条</td>
		</tr>
	</tbody>
</table>
实时行情服务器向终端回应消息格式如下：
<table class="table table-bordered">
	<thead>
		<tr>
			<th style="width: 200px;">接口名称</th>
			<th>字段名称</th>
			<th style="width: 60px;">是否可选</th>
			<th>字段值</th>
			<th>字段说明</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<th rowspan="6">获取Top行情深度</th>
			<th>version</th>
			<td>必选</td>
			<td>1</td>
			<td>终端版本</td>
		</tr>
		<tr>
			<th>msgType</th>
			<td>必选</td>
			<td>reqTradeDetailTop</td>
			<td>消息类型</td>
		</tr>
		<tr>
			<th>requestIndex</th>
			<td>可选</td>
			<td>100</td>
			<td>请求序列号，方便判断多个请求的先后顺序，终端发送的数据，服务端会返回相同的数据</td>
		</tr>
		<tr>
			<th>retCode</th>
			<td>必选</td>
			<td>200</td>
			<td>返回错误码，200为成功，其他的参照http返回码</td>
		</tr>
		<tr>
			<th>retMsg</th>
			<td>必选</td>
			<td></td>
			<td>返回消息</td>
		</tr>
		<tr>
			<th>payload</th>
			<td>必选</td>
			<td></td>
			<td>有效数据</td>
		</tr>
	</tbody>
</table>

####10)	获取盘口信息


	reqMarketDetail该消息用于获取完整的行情深度。<br>
	终端向实时行情服务器请求消息格式如下：

<table class="table table-bordered">
	<thead>
		<tr>
			<th style="width: 200px;">接口名称</th>
			<th>字段名称</th>
			<th style="width: 60px;">是否可选</th>
			<th>字段值</th>
			<th>字段说明</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<th rowspan="4">获取盘口信息</th>
			<th>version</th>
			<td>必选</td>
			<td>1</td>
			<td>终端版本</td>
		</tr>
		<tr>
			<th>msgType</th>
			<td>必选</td>
			<td>reqMarketDetail</td>
			<td>消息类型</td>
		</tr>
		<tr>
			<th>requestIndex</th>
			<td>可选</td>
			<td>100</td>
			<td>请求序列号，方便判断多个请求的先后顺序，终端发送的数据，服务端会返回相同的数据</td>
		</tr>
		<tr>
			<th>symbolId</th>
			<td>必选</td>
			<td>btccny</td>
			<td>交易代码列表，1个到多个交易编码。</td>
		</tr>
	</tbody>
</table>
实时行情服务器向终端回应消息格式如下：
<table class="table table-bordered">
	<thead>
		<tr>
			<th style="width: 200px;">接口名称</th>
			<th>字段名称</th>
			<th style="width: 60px;">是否可选</th>
			<th>字段值</th>
			<th>字段说明</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<th rowspan="6">获取盘口信息</th>
			<th>version</th>
			<td>必选</td>
			<td>1</td>
			<td>终端版本</td>
		</tr>
		<tr>
			<th>msgType</th>
			<td>必选</td>
			<td>reqTradeDetailTop</td>
			<td>消息类型</td>
		</tr>
		<tr>
			<th>requestIndex</th>
			<td>可选</td>
			<td>100</td>
			<td>请求序列号，方便判断多个请求的先后顺序，终端发送的数据，服务端会返回相同的数据</td>
		</tr>
		<tr>
			<th>retCode</th>
			<td>必选</td>
			<td>200</td>
			<td>返回错误码，200为成功，其他的参照http返回码</td>
		</tr>
		<tr>
			<th>retMsg</th>
			<td>必选</td>
			<td></td>
			<td>返回消息</td>
		</tr>
		<tr>
			<th>payload</th>
			<td>必选</td>
			<td></td>
			<td>有效数据</td>
		</tr>
	</tbody>
</table>