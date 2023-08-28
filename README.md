### 示例框架

ThinkPHP 5.1

### 官方文档

<a href="https://developers.weixin.qq.com/doc/offiaccount/Message_Management/Message_encryption_and_decryption_instructions.html" target="_blank" title="消息加解密说明">消息加解密说明</a>

### 下载地址

![image](https://github.com/itinfor/wechat_msg_crypt/assets/46643783/cbf00dc0-35f3-4065-9932-a6fcc247e44e)

### 封装说明

追加了命名空间+格式化文件


### 使用方法

1、在项目根目录执行 **composer require itinfor/wechat_msg_crypt**，安装该插件

2、安装完成，在vendor目录下，可以看到下载的文件，如下图所示：

![image](https://github.com/itinfor/wechat_msg_crypt/assets/46643783/24483a41-33c6-49e8-a76f-1710781943d0)

3、在文件顶部需要通过use引入：

![image](https://github.com/itinfor/wechat_msg_crypt/assets/46643783/35dbf790-0925-4ae2-b0c8-5e3d7b0fcc95)
```
use Itinfor\WXBizMsgCrypt;
```

4、在需要的调用的地方，跟官方文档一样引用即可，如下：

![image](https://github.com/itinfor/wechat_msg_crypt/assets/46643783/b89e7046-2024-44f7-b201-90b0e4ddd1a8)
```
$WXBizMsgCrypt = new WXBizMsgCrypt($token, $encodingAesKey, $appId);
```

5、解密：

![image](https://github.com/itinfor/wechat_msg_crypt/assets/46643783/dc0bd13a-6469-4318-a460-e17ed24a7238)

```
Log::info("get===============>" . json_encode($_GET));
if ( ! empty($_GET['msg_signature']) && ! empty($_GET['timestamp']) && ! empty($_GET['nonce']))
{
    $errCode = $WXBizMsgCrypt->decryptMsg($_GET['msg_signature'], $_GET['timestamp'], $_GET['nonce'], $from_xml, $msg);
    Log::info("errCode============>" . $errCode);
    Log::info("msg============>" . $msg);

    $object_xml = simplexml_load_string($msg, 'SimpleXMLElement', LIBXML_NOCDATA);//将文件转换成对象
    $xml_json = json_encode($object_xml);//将对象转换个JSON

    Log::info("xml_json===========>" . $xml_json);
}
```




