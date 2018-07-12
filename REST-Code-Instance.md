## 代码示例
火币目前提供了JAVA、PHP、Python版本的代码示例，下载地址：https://github.com/huobiapi?tab=repositories<br>
其他语言会根据需要相继支持。在使用过程中有任何问题请联系我们的API技术讨论QQ群，我们将在第一时间帮您解决技术问题。

以下是PHP代码示例
```php
<?php

// 密匙对
define('ACCESS_KEY', 'xxxxxxxx-xxxxxxxx-xxxxxxxx-xxxxx');
define('SECRET_KEY', 'xxxxxxxx-xxxxxxxx-xxxxxxxx-xxxxx');

// 使用 apiv3
define('API_URL', 'https://api.huobi.com/apiv3');

function httpRequest($pUrl, $pData){
	$tCh = curl_init();
	if($pData){
		is_array($pData) && $pData = http_build_query($pData);
		curl_setopt($tCh, CURLOPT_POST, true);
		curl_setopt($tCh, CURLOPT_POSTFIELDS, $pData);
	}
	curl_setopt($tCh, CURLOPT_HTTPHEADER, array("Content-type: application/x-www-form-urlencoded"));
	curl_setopt($tCh, CURLOPT_URL, $pUrl);
	curl_setopt($tCh, CURLOPT_RETURNTRANSFER, true);
	curl_setopt($tCh, CURLOPT_SSL_VERIFYPEER, false);
	$tResult = curl_exec($tCh);
	curl_close($tCh);
	$tmp = json_decode($tResult, 1);
	if($tmp) {
		$tResult = $tmp;
	}
	return $tResult;
}

function createSign($pParams = array()){
	$pParams['secret_key'] = SECRET_KEY;
	ksort($pParams);
	$tPreSign = http_build_query($pParams);
	$tSign = md5($tPreSign);
	return strtolower($tSign);
}

function send2api($pParams, $extra = array()) {
	$pParams['access_key'] = ACCESS_KEY;
	$pParams['created'] = time();
	$pParams['sign'] = createSign($pParams);
	if($extra) {
		$pParams = array_merge($pParams, $extra);
	}
	$tResult = httpRequest(API_URL, $pParams);
	return $tResult;
}

function getAccountInfo(){
	$tParams = $extra = array();
	$tParams['method'] = 'get_account_info';
	// 不参与签名样例
	// $extra['test'] = 'test';
	$tResult = send2api($tParams, $extra);
	return $tResult;
}

try {
	var_dump(getAccountInfo());
} catch (Exception $e) {
	var_dump($e);
}
```