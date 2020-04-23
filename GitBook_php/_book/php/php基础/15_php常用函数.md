# PHP常用函数

| 函数名          | 描述                                                         |
| --------------- | ------------------------------------------------------------ |
| exit(string)    | 是直接停止，并且不运行后续代码，exit()可以显示内容           |
| die(string)     | 是遇到错误才停止 opendir('./upload-from') or die('哦哦,出问题') |
| md5(string,raw) | 计算字符串的 MD5 散列                                        |

## JSON 函数

| 函数名      | 描述                                          |
| ----------- | --------------------------------------------- |
| json_encode | 对变量进行 JSON 编码                          |
| json_decode | 对 JSON 格式的字符串进行解码，转换为 PHP 变量 |

## PHP字符串函数

### substr --- 取得部份字符串

> substr()截取字符串出现乱码问题该怎么办？

在PHP程序开发中，经常会执行字符串的截取操作，比如输出信息列表时，标题不宜过长，打印文章摘要时，也要执行一系列的字符串截取操作。遇到这些需求时，我们经常会想到使用substr()方法来实现，substr()对全英文字符串的截取是比较适合的。

但字符串只要出现中文字符，就有可能导致PHP substr中文乱码，因为中文UTF-8编码，每个汉字占3字节，而GB2312占2字节，英文占1字节，截取位数不准确，substr()硬生生地将一个中文字符“锯”成两半，造成断开的字符会把其后的..拉过来一起做一个字，所以出现了PHP substr中文乱码。

语法 :

```
string substr (string string, int start [, int length])
```

说明 : substr( )传回 string的一部份字符串，由参数 start和 length指定。

如果 start是正数，传回的字符串将会从 string的第 start个字元开始。

#### mbstring扩展库

使用mbstring扩展库的`mb_substr()`截取就不会出现乱码了。

可以用`mb_substr()/mb_strcut()`这个函数，`mb_substr()/mb_strcut()`的用法与`substr()`相似，只是在`mb_substr()/mb_strcut`最后要加入多一个参数，以设定字符串的编码，但是一般的服务器都没打开php_mbstring.dll，需要在php.ini在把php_mbstring.dll打开。

```
<?php
  echo mb_substr("php中文字符encode",0,4,"utf-8");
?>
```

如果未指定最后一个编码参数，会是三个字节为一个中文，这就是utf-8编码的特点，若加上utf-8字符集说明，所以，是以一个字为单位来截取的。

## PHP mail() 函数

PHP mail() 函数用于从脚本中发送电子邮件。 语法 mail(to,subject,message,headers,parameters)

| 参数       | 描述                                                         |
| ---------- | ------------------------------------------------------------ |
| to         | 必需。规定 email 接收者。                                    |
| subject    | 必需。规定 email 的主题。注释：该参数不能包含任何新行字符。  |
| message    | 必需。定义要发送的消息。应使用 LF (\n) 来分隔各行。每行应该限制在 70 个字符内。 |
| headers    | 可选。规定附加的标题，比如 From、Cc 和 Bcc。应当使用 CRLF (\r\n) 分隔附加的标题。 |
| parameters | 可选。对邮件发送程序规定额外的参数。                         |

```php
<?php
$to = "someone@example.com";         // 邮件接收者
$subject = "参数邮件";                // 邮件标题
$message = "Hello! 这是邮件的内容。";  // 邮件正文
$from = "someonelse@example.com";   // 邮件发送者
$headers = "From:" . $from;         // 头部信息设置
mail($to,$subject,$message,$headers);
echo "邮件已发送";
?>
```