## 下载抽取API
### 1. 接口描述
  域名：wenzhi.api.qcloud.com
  接口名: ContentGrab
	
  下载接口基于分布式爬虫系统，用户只需提供一个url即可轻松完成数据抓取, 也可与下载团队合作打造专有的定向抓取服务。分布式爬虫系统通过对全网 url 进行精准调度、智能压力挖掘、自适应页面更新周期预测，可以实现自动路由、url 作弊识别、智能主题抓取等功能。扁平的架构设计使得系统可以进行任意的扩展，同时结合公司海量运营的经验，在系统监控、运营告警等方面都不断进行完善使得系统可以稳定高效运行。
  抽取接口支持 Html 网页的标题、正文等十数种重要字段的抽取，以及特殊类型网页的定制化抽取服务。抽取后台完成网页内容的归一化、结构化处理工作，用户只需要调用抽取 API 即可高效完成从指定页面获得丰富的结构化信息。目前已经接入业务包括网页转码、广点通等。
### 2.输入参数
<table class="t">
<tr>
<th width="50"> <b>参数名称</b>
</th><th width="50"> <b>必选</b>
</th><th width="80"> <b>类型</b>
</th><th width="100"> <b>描述</b>
</th></tr>
<tr>
<td> url </td><td>  是 </td><td> String </td><td> 待抓取的 url
</td></tr></table>

### 3. 输出参数
<table class="t">
<tr>
<th width="80"> <b>参数名称</b>
</th><th width="80"> <b>必选</b>
</th><th width="100"> <b>描述</b>
</th></tr>
<tr>
<td> code </td><td> Int32 </td><td> 错误码, 0: 成功, 其他值: 失败
</td></tr>
<tr>
<td> message </td><td> String </td><td> 错误信息
</td></tr>
<tr>
<td> title </td><td> String </td><td> 返回输入 uri 对应网页的标题
</td></tr>
<tr>
<td> content </td><td> String </td><td> 返回输入 uri 对应网页的正文
</td></tr></table>

  下载抽取API错误码详细信息如下：
<table class="t">
<tr>
<th width="50"> <b>错误码</b>
</th><th width="100"> <b>含义说明</b>
</th></tr>
<tr>
<td> 400 </td><td> HTTP Method不正确
</td></tr>
<tr>
<td> 401 </td><td> HTTP请求参数不符合要求
</td></tr>
<tr>
<td> 503 </td><td> 调用额度已超出限制
</td></tr>
<tr>
<td> 504 </td><td> 服务故障
</td></tr></table>

### 4. 详细示例
  示例业务详细信息如下表：
<table class="t">
<tr>
<th width="100"> <br />
</th><th width="80"> <b>参数名称</b>
</th><th width="100"> <b>参数描述</b>
</th><th width="50"> <b>必选</b>
</th><th width="150"> <b>参数值示例</b>
</th></tr>
<tr>
<td rowspan="4">腾讯云公共参数 </td><td> Action </td><td> 方法名 </td><td> 是 </td><td> ContentGrab
</td></tr>
<tr>
<td> SecretId </td><td> SecretId </td><td> 是 </td><td> AKIDz8krbsJ5yKBZQpn74WFkmLPx3gnPhESA
</td></tr>
<tr>
<td> Timestamp </td><td> 当前时间戳 </td><td> 是 </td><td> 1408704141
</td></tr>
<tr>
<td> Nonce </td><td> 随机正整数 </td><td> 是 </td><td> 345122
</td></tr>
<tr>
<td> 业务参数 </td><td> url </td><td> 待抓取的url </td><td> 是 </td><td>http://www.qq.com
</td></tr></table>


  下面以上述业务为例，详细说明“下载抽取 API”接口的使用方法。
#### 4.1 接口鉴权
  示例要调用服务的数据为：{"url":"`http://www.qq.com`"}
  则上述业务的参数列表如下：
 
 <div class="code">
 <pre> {
        'Action' : 'ContentGrab',
        'Nonce' : 345122,
        'Region' : 'sz',
        'SecretId' : 'AKIDz8krbsJ5yKBZQpn74WFkmLPx3gnPhESA',
        'Timestamp' : 1408704141,
        'url': 'http://www.qq.com'
    }</pre>
</div>

  根据上述参数列表进行签名，得出的数字签名为：HgIYOPcx5lN6gz8JsCFBNAWp2oQ（示例），详细的数字签名的生成方法请参照：《腾讯云接口鉴权》。
 <b> 注意：</b>
  1）在生成签名的过程中，需要将加密字符串中包含的“_”改写成“.”，从而加密产生签名；
  2）鉴权时，需要将参数列表按key进行排序：字典序，同时大写在前。
#### 4.2 API调用
  根据上一步（8.4.1）中得到的数字签名，以POST请求为例构造请求URL，将数字签名加入到参数Signature中。
 
 <div class="code">
 <pre>  https://wenzhi.api.qcloud.com/v2/index.php?
	Action=ContentGrab
	&Nonce=345122
	&Region=sz
	&SecretId=AKIDz8krbsJ5yKBZQpn74WFkmLPx3gnPhESA
	&Timestamp=1408704141
	&Signature=HgIYOPcx5lN6gz8JsCFBNAWp2oQ
	&url=http://www.qq.com</pre>
</div>

  执行上述操作之后，会将数据{"url":"`http://www.qq.com`"} 发送给API接口，进行相应分析。
 <b> 注意：</b>在发送请求过程中，不能将参数字符串中包含的“”改写成“.”。
