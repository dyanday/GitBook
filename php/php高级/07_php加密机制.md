# 加密机制

### PHP中的几种加密方式

- md5()加密算法
- crypt()加密算法
- sha1()加密算法
- URL编码加密技术
- Base64编码加密技术

### md5()加密算法

计算str的md5散列值

```php
string md5( string $str [, bool $raw_output = false ])
```

参数

| 参数        | 描述                                                         |
| :---------- | :----------------------------------------------------------- |
| $str        | 原始字符串                                                   |
| $raw_output | 返回以32位字符十六进制形式返回(设置为true，那么md5摘要将以16字节长度的原始二进制格式返回) |

> MD5加密已经不安全了，我们可以通过2次md5的结果来强化密码安全性。

MD5的加密方式目前已经不太安全了，因为它的加密算法实在是显得有点简单了，而且很多破解密码的站点都存放了很多经过MD5加密的密码字符串，所以不提倡还在单单使用MD5来加密用户的密码的。

### crypt()加密算法

返回一个基于标准UNIX DES算法或系统上其它可用的替代算法的散列字符串。

```
string crypt(string $str [,string $salt])
```

参数

| 参数  | 描述                          |
| :---- | :---------------------------- |
| $str  | 原始字符串                    |
| $salt | 加密时的干扰串,使得编码更安全 |

### sha1()加密算法

计算字符串的sha1散列值

```
string sha1(string $str [,bool $raw_output=false]);
```

参数

| 参数        | 描述                                                         |
| :---------- | :----------------------------------------------------------- |
| $str        | 原始字符串                                                   |
| $raw_output | 返回以40位字符十六进制形式返回(设置为true，那么sha1摘要将以20字符长度的原始二进制格式返回) |

### URL编码加密技术

#### urlencode 编码URL字符串

```php
string urlencode(string $str)
```

$str 要编码的字符串

返回值：返回编码后的字符串

编码规范：此字符串中除了 `-_.`之外的所有非字母数字字符都将被替换成百分号(%)后跟两位十六进制数，空格则编码为加号(+)

#### urldecode 解码已编码的URL字符串

```php
string urldecode(string $str)
```

$str 要解码的字符串

返回值：返回解码后的字符串

#### rawurlencode 编码URL字符串

按照RFC1738对URL进行编码

```php
string rawurlencode(string $str)
```

$str 要编码的字符串

返回值：返回编码后的字符串，把空格编码为%20

#### rawurldecode 解码已编码的URL字符串

```php
string rawurldecode(string $str)
```

$str 要解码的字符串

返回值：返回解码后的字符串